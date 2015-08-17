---
title: "Setting up DNS service discovery in kubernetes"
layout: post
date: 2015-08-13 19:33:37 CEST
published: true
categories:
---

The usual way to set up service discovery in kubernetes is through environment
variables, which are made available to all the Docker containers launched
inside pods across the system. But another (and arguably more simplistic and elegant) way
to handle service discovery is through DNS.

Kubernetes offers a cluster addon for DNS service discovery, which most
environments enable by default. [SkyDNS](https://github.com/skynetservices/skydns)
seems to be the standard DNS server of choice, since it was designed to work on
top of etcd.  The `kube-dns` addon is composed of a kubernetes service which,
like all services, is allocated an arbitrary VIP within the preconfigured subnet
(this is the IP that every other service will use for DNS); and a replication
controller that will manage pods with the following containers inside them:

- a local etcd instance
- the SkyDNS server
- a process called [kube2sky](https://github.com/kubernetes/kubernetes/tree/master/cluster/addons/dns/kube2sky) which binds SkyDNS to the kubernetes cluster
- a health check called [healthz](https://github.com/kubernetes/kubernetes/tree/master/pkg/healthz) that monitors how DNS is being resolved

In order to set everything up, you will need to retrieve the definition files
for the service and replication controller, like so:

{% highlight bash %}
curl -sO https://gist.githubusercontent.com/jamiehannaford/b80465bf7d427b949542/raw/75e7c0ff3fc740ea0f4eb54e5d10753cccf1267b/skydns-svc.yml
{% endhighlight %}
{% highlight bash %}
curl -sO https://gist.githubusercontent.com/jamiehannaford/850900e2d721a973bc6d/raw/710eade5b8d5a382cdc6d605d6cd2d43fb0c20fb/skydns-rc.yml
{% endhighlight %}

You will then need to edit ``skydns-rc.yaml`` so that the ``MASTER_IP`` placeholder
is replaced with the IP of your kubernetes master node:

{% highlight bash %}
sed -i -e '/s/MASTER_IP/xxx.xxx.xxx.xxx/g' skydns-rc.yaml
{% endhighlight %}

I've assumed that the `kube-dns` addon will use a service IP of ``10.1.0.10``. If this
does _not_ correspond to your own subnet range, you can replace this value in
``skydns-svc.yaml``. The second assumption is that ``kube.local`` will be used as the DNS domain. You will need to
replace all occurrences in ``skydns-rc.yaml`` if you want it any other way.
Once you're happy, you can start all the services:

{% highlight bash %}
kubectl create -f skydns-rc.yaml
kubectl create -f skydns-svc.yaml
{% endhighlight %}

This will create a replication controller and service under the ``kube-system``
namespace. To check their status, run:

{% highlight bash %}
kubectl get pods --namespace=kube-system
kubectl get services --namespace=kube-system
{% endhighlight %}

Once your pod is completely up-and-running, you will need to pass in the DNS server IP and domain to all of the
kubelet agents running on your minion hosts. To do this, you will likely need
to change the local systemd unit files on your minions. You will need to add the following flags to the command specified in the ``ExecStart`` block:

{% highlight bash %}
--cluster-dns=10.1.0.10
--cluster-domain=kube.local
{% endhighlight %}

To test that it's working, create a file named `busybox.yaml` containing:

{% highlight yaml %}
apiVersion: v1
kind: Pod
metadata:
  name: busybox
  namespace: default
spec:
  containers:
  - image: busybox
    command:
      - sleep
      - "3600"
    imagePullPolicy: IfNotPresent
    name: busybox
  restartPolicy: Always
{% endhighlight %}

and create it in kubernetes:

{% highlight bash %}
kubectl create -f busybox.yaml
{% endhighlight %}

This should provision the above pod on a minion configured to use the DNS
service we have just set up. To test that this is so, you can run:

{% highlight bash %}
kubectl exec busybox -- nslookup kubernetes
{% endhighlight %}

You can substitute `kubernetes` any service name that is currently running, and it will
resolve to the IP of a pod that the service ordinarily directs to. And that's it,
happy hacking!
