---
layout: post
title: "Why you should consider BDD for OSS"
date: 2014-02-15 22:47
published: false
tags: bdd oss
---


Whenever I hear or read something about BDD, references are always made to the stakeholders of a project. This is for good reason: BDD, after all, is a methodology to promote better communication - it aims to bridge the technical divide between team members and put the customer’s requirements at the forefront of development. 

But for open-source developers, this leaves us in an awkward position. The objectives of BDD all sound fine and dandy, but how do we reconcile them with the modern reality of free and open codebases? How can a dissipated and "unknown" user-base become the center of what we do? Is BDD even applicable to open-source at all?

The answer, in my opinion, is a definitive Yes.

# Specs and stories

Before I elaborate on my reasoning, it’d be useful to refresh our memory and define how BDD works. Behavior-driven development is usually applied in two different ways: SpecBDD and StoryBDD. Both represent, and are subsets of, the wider methodology, but their scope is different.

SpecBDD is easy to define, since it's all there in the name: it is a technique of describing functionality at the object level in small iterative steps. The workflow is simple: you specify behaviour first, then implement just enough code to satisfy that specification, and then refactor. It is roughly analogous to TDD, but behaviour is at the heart of development.

Defining these behaviour first allows you to clarify your direction and make the time you spending implementing the details more focused and efficient. Because you've thought about the problem beforehand and reified it with concrete language, you have a clearer vision of the solution. Design becomes emergent, instead of an afterthought. It's for this reason that Kent Beck considers writing specications a fear management technique. And that's completely true: you're no longer meandering through development without a clear direction. SpecBDD allows us to crystallize our ideas of how something works first, and then spend just enough of our time and resources to get that working.

Whilst SpecBDD covers how to describe behavior at the object level, StoryBDD describes the behavior of features at the domain or business level. Whereas SpecBDD is microscopic, StoryBDD is macroscopic.

The general idea is to make sure that our software actually solves the business problems that our customers are facing. We open up the dialogue, we listen to what their requirements are, we distill those requirements into blueprints that can realistically achieve this functionality, then we code and make those blueprints a reality. The organic result of this approach is the production of software _that actually matters_.

So, at the heart of this process, is feature stories. Feature stories are human-readable specifications of features that _everyone_ can understand. You don't need a complex understanding of a language, you don't need to be an API witch doctor, you don't need a neck beard. Everyone's on a level field.

Each story defines how a feature works through examples. These examples (also called scenarios), serve multiple purposes. Apart from their important role of communicating the intent of a feature, they can also be executed by tools and serve as functional tests: they become benchmarks of project progress. They can be thought of as living, executable documentation.

# So why are stories useful for my OSS project?

There is a big difference between software produced for clients and software released to an open-source community. With client work, you write software and invoice it - you directly monetize your output. But OSS is centered on completely opposite principles: monetization is completely against its raison d'etre. Instead, people write and release their work for free, for the altruistic benefit of prospective users. So if BDD is all about investing your software with business value, how does this work with open-source? What drives value in the OSS community?

The answer is People. People make open-source work: they write the code, they review patches, they download and install the software, they file the bug reports, they contribute back. The value of open-source is attained through how many people adopt your work and contribute back to it. 

So, when we look at it this way, the value of your OSS project is completed interwoven with the concerns of your user-base. And it’s this realization which shows us how important BDD is to our projects, because:

- BDD allows us to understand, and directly connect with, our user-base. They are the stakeholders who give value our open-source enterprise;

- BDD ensures that every feature we write produces some measurable benefit to our stakeholders;

- BDD improves collaboration because there is a clear, concise way to articulate new or modified functionality.

- BDD improves communication for everyone involved in the project because there is a ubiquitous language that does not rely on previous experience, knowledge or skill

BDD removes fuzzy or implicit assumptions of what we _think_ our users want with concrete requirements. By having the conversation, we now actually understand what we're writing, and who we're writing for. I'd guess that the majority of projects, especially OSS, don't differentiate those using their product. Not all developers are the same. Not all businesses are the same.

# How do we know what features the OSS community wants?

I think a more useful question would be this: How do we facilitate understanding in OSS projects?

Well, answering this question isn't that hard. In order to understand what our users want, we need to talk with them. At the kernel of BDD is conversation and communication - it drives the whole process.

So how do we talk to and understand what the users of our software want?

- Go through Github issues to find common problems and feature requests
- Use issues, PRs, tweets, e-mails, IRC threads to see what components or features people are most interested in
- Filter these channels to get the general gist of what our customers are saying - what are their individual use cases? Are there patterns?

Once we have some idea of what our customers want, and we've translated those requirements into Gherkin features, we now have a mandate for implementation. One of the cool outcomes of such a process is that we're able to challenge our own assumptions of what value means to our users. We should not write features that are based on our _own_ assumptions (i.e. what we think is valuable), it should always be end-user focused.

And if you have no metrics whatsoever, it’s okay to make educated guesses. If you yourself are a prospective user, feel free to use your own experience of interacting with similar products to inform how a new piece of software will work. Then collaborate with similar users to deepen your understanding. Start those conversations, enrich your scenarios with real content.

Henry Ford once said that "If I had asked people what they wanted, they would have said faster horses." Perhaps that's true, but so is this: people drive innovation, not singular individuals. In one of his more famous meditations, John Donne said this:

> No man is an island,  entire of itself; every man is a piece of the continent, a part of the main

And isn't that what open-source software is all about? Driving great products through open dialogue and collaboration? Sharing ideas and challenging existing ones? Building and breaking things in a shared enterprise, for the benefit of all, not just one.
