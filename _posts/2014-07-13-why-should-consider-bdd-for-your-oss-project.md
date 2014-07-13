---
layout: post
title: "Why you should consider BDD for your OSS project"
date: 2014-07-13 19:47
published: true
tags: bdd oss
---

Whenever I hear or read something about BDD, references are always made to the stakeholders of a project. This is for good reason: BDD, after all, is a methodology to promote better communication - it aims to bridge the technical divide between team members and put the customer’s requirements at the forefront of development. 

But for open-source developers, this leaves us in an awkward position. The objectives of BDD all sound fine and dandy, but how do we reconcile them with the modern reality of free and open codebases? How can a dissipated and "unknown" user-base become the center of what we do? Is BDD even applicable to open-source at all?

The answer, in my opinion, is a definitive Yes.

## What is BDD?

Before I elaborate on my reasoning, it’d be useful to refresh our memory and define how BDD works. Behavior-driven development is usually applied in two different ways: SpecBDD and StoryBDD. Both represent, and are subsets of, the wider methodology, but their scope is different.

### Specs

SpecBDD is easy to define, since it's all there in the name: it is a technique of describing functionality at the object level in small iterative steps. The workflow is simple: you specify behaviour first, then implement just enough code to satisfy that specification, and then refactor. It is roughly analogous to TDD, but behaviour is at the heart of development.

Defining behaviour first allows you to clarify direction and make the time you spending implementing the details more focused and efficient. Because you've thought about the problem beforehand - and reified it into a specification with concrete language - you have a clearer vision of what the solution might look like. Forethought allows good design to become an imminent priority, instead of an inconvenient afterthought that only mitigates the damage of code slinging.

It's for this reason that Kent Beck considers writing specs a fear management technique. And that's completely true: you're no longer meandering through development without a clear direction. SpecBDD allows us to crystallize our ideas of how something works first, and then spend just enough of our time and resources to get that working.

### Stories

Whilst SpecBDD covers how to describe behavior at the object level, StoryBDD describes the behavior of features at the domain or business level. SpecBDD is microscopic, StoryBDD is macroscopic.

The general idea of StoryBDD is to make sure that software actually solves the business problems that customers are facing. We open up the dialogue, we listen to what their requirements are, we distill those requirements into blueprints that can realistically achieve this functionality, then we code and make those blueprints a reality. The organic result of this approach is software _that actually matters_.

In order to make this a reality, we have feature stories. Feature stories are human-readable specifications of features that _everyone_ on the team can understand. Because they're written in the Gherkin syntax, the workings of a feature become easily understood. You don't need a complex understanding of a language; you don't need to be an API witch doctor; you don't need a neck beard. Knowledge is no longer shut off and cabalistic, it's open for everyone to understand and contribute back to.

Each story defines how a feature works through examples. These examples (also called scenarios), serve multiple purposes. Apart from their important role of communicating the intent of a feature, they can also be executed by tools like Cucumber and Behat to serve as functional tests. The tools parse the syntax and run the examples, allowing them to become benchmarks of project progress. I like to think of feature stories as living documentation that can be _executed_.

## So why are stories useful for my OSS project?

There is a big difference between software produced for clients and software released to an open-source community. With client work, you write software and invoice it - you directly monetize your output. But OSS is based on opposite principles: monetization is completely against its raison d'etre. Instead, people write and release their work for free, for the altruistic benefit of prospective, unseen users. 

So, here's the quandary: if BDD is all about investing your software with business value, how does this work for projects which aren't fiscally motivated? What drives value in the OSS community?

The answer is People. People make open-source work: they write the code, they review patches, they download and install the software, they file the bug reports, they contribute back. The value of open-source is attained through how many people adopt your work and contribute back to it. 

So, when we look at it this way, the value of your OSS project is completed interwoven with the concerns of your user-base. And it’s this realization which shows us how important BDD is to our projects, because:

- BDD allows us to understand, and directly connect with, our user-base. Our feature stories are more than stale blueprints: they're active promises of how features will work;

- BDD ensures that our time and effort is well spent. Stories allow us to measure how we spend our time and ensure that our code delivers value;

- BDD improves collaboration and communication because there is a clear, concise way to articulate new or modified functionality. It democratizes the process of defining features, because nobody needs an intricate knowledge of the codebase to grok how it works.

Not all developers are the same. Not all businesses are the same. BDD removes fuzzy or implicit assumptions of what we _think_ our users want with concrete requirements that can be executed and verified.

## How do we know what features the OSS community wants?

I think a more useful question would be this: How do we facilitate understanding in OSS projects?

Well, in order to understand what our users want, we need to talk with them. But how do we talk to and understand what the users of our software want? It really depends on the nature of your project, but you can:

- Go through old issues to find common problems and feature requests. What currently doesn't work? Are there frequent complaints that expose misaligned expectations?

- Open up communication channels. Use issue trackers, forums, patches, tweets, e-mails, IRC threads, to see what functionality people are most interested in. How do they expect it to work? Are you addressing those needs?

- Use quantative data and metrics, if available. If you're running an API - see whether you can pin down logfiles. If you have an OSS package comprised of components, can you track component downloads? Do you have Analytics data for the most popular documentation pages? If not, could you start doing this?

Once you have some idea of what your customers want, translate those requirements into feature stories and produce your mandate for implementation. One of the cool outcomes is that you'll soon challenge your own assumptions of what value actually means to your users. We shouldn't write features that are based on our _own_ assumptions (i.e. what we think is valuable), it should always be end-user focused.

And if you have no metrics whatsoever, it’s okay to make educated guesses. If you yourself are a prospective user, feel free to use your own experience of interacting with similar products to inform how a new piece of software will work. Then collaborate with similar users to deepen your understanding. Start those conversations, enrich your scenarios with real content.

## Should we trust users?

Henry Ford once said that "If I had asked people what they wanted, they would have said faster horses." Perhaps that's true, but so is this: people drive innovation, not singular individuals. In one of his more famous meditations, John Donne said:

> No man is an island,  entire of itself; every man is a piece of the continent, a part of the main

Isn't that what open-source software is all about? Driving great products through open dialogue and collaboration? Sharing ideas and challenging existing ones? Building and breaking things in a shared enterprise, for the benefit of all, not just one.
