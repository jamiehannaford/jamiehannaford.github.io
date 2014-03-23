---
title: "Logging with PSR-3"
layout: post
date: 2014-02-25 21:15:14 CET
published: true
categories: php fig logging
---

One of the cool things [PSR-FIG](http://www.php-fig.org/) has given the PHP community is a bunch of standardised interfaces for logging messages. This basically means there’s no longer an excuse for having three dozens different ways of implementing the same piece of logic or functionality.

## Setup

To take advantage of these standard interfaces, you will need to add the `psr/log` package as a Composer dependency:

{% highlight json %}
"require": {
   "psr/log": "1.0"
}
{% endhighlight %}

## Basic usage

If you have a quick butchers at the PSR-3 [example repository](https://github.com/php-fig/log), you’ll see that they do not provide a concrete logging class - only an interface and an abstract one. They leave the implementation up to you because the `log` method can differ so greatly.

So the first thing you will need to do is define your own concrete class:

{% highlight php startinline %}
use Psr\Log\AbstractLogger;

class MyLogger extends AbstractLogger
{
   public function log($level, $message, array $context = [])
   {
      echo strtr($message, $context);
   }
}
{% endhighlight %}

Using the [`strtr`](php.net/strtr) function you can easily populate a string with an array of context variables. One example might be:

{% highlight php startinline %}
$logger->log(LogLevel::EMERGENCY, '{thing} is broken! Notify {duty_dev}', [
   '{thing}'    => 'MySQL master',
   '{duty_dev}' => 'Sarah'
]);
{% endhighlight %}

As you will notice, the first argument is a class constant which defines the level, or severity, of log message being emitted. For a full list, please consult the [`LogLevel`](https://github.com/php-fig/log/blob/master/Psr/Log/LogLevel.php) class.

## Mix it up

We're echoing stuff, cool. But that's not great for all use cases. What if we want the added flexibility of logging to the filesystem *and* stdout? Well, we can do that very easily:

{% highlight php startinline %}
class MyLogger extends AbstractLogger
{
    /** @var resource The stream resource being written to */
    protected $stream;

    public function __construct()
    {
        // handle basic use-case
        $this->stream = STDERR;
    }

    public function setStream($stream)
    {
        $this->stream = $stream;
    }

    public function log($level, $message, array $context = [])
    {
        fwrite($this->stream, strtr($message, $context));
    }
}
{% endhighlight %}

The function [`fwrite`](http://php.net/fwrite) writes a string message to any stream specified, whether it be to the local filesystem or to standard output. You will notice that [`STDERR`](http://www.php.net/manual/en/features.commandline.io-streams.php) is used as the default stream. This is simply a constant which represents the stream resource: `fopen('php://stderr', 'w');`

You'd then access this from your main script:

{% highlight php startinline %}
class MyBeautifulApp
{
    public function handleError(ErrorInterface $e)
    {
        $stream = fopen('/log/errors.log', 'a');
        $this->logger->setStream($stream);
        
        $this->alertDevelopers();
        $this->logger->critical("We're being DDOSed by hackers from {source}", [
            '{source}' => $e->getAttackSource()
        ]);
        
        fclose($stream);
    }
}
{% endhighlight %}

The PSR's [abstract logger](https://github.com/php-fig/log/blob/master/Psr/Log/AbstractLogger.php) offer eight different logging methods (one for each severity type), which basically just invokes the `log` method will the appropriate LogLevel type passed in.

## Conclusion

Awesome! I've implemented a standardised solution for logging that will allow my app to output errors in a consistent and well-thought-out manner. I've also baked in the ability to output dynamically to different locations - to the local filesystem or standard streams like `STDERR` or `STDOUT`.