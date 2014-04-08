---
title: "7 reasons why you should use phpspec"
layout: post
date: 2014-04-08 18:29:12 CEST
published: true
tags: bdd testing
categories: code
---
1. *It allows your code to align perfectly with project expectations.* By specifying the behaviour of your class, it allows you to directly map what you're coding to the described specifications of your project. You don't have to drift aimlessly: you can instead ensure what you're speccing directly aligns with established end-user expectations. In other words, every single piece of code you write has measurable business value - you're not wasting energy or time. You're always focused and on-track.

2. *It enforces good design.* You can get away with murder in phpunit - it doesn't really do much to nudge you in the right direction. [phpspec](http://phpspec.net/) on the other hand makes it very difficult to get away with bad design. By making certain bad practices extremely difficult to implement, it forces you to continually think about good design. Dependency injection, for example, is an important concept in phpspec. After using this tool for 2 weeks, my code became cleaner because I was forced to think about good design from the very beginning. It was no longer an afterthought.

3. *It forces you to think about collaborators.* In phpunit, everything executes like it would in a normal thread of execution. Which is bad because it makes you complacent on things "just working", when really you could have no idea what's happening beneath the surface. [Prophecy](https://github.com/phpspec/prophecy), a powerful mocking framework which backs phpspec, forces you to define how your class behaves with collaborators. If you're testing a piece of behaviour that relies on the response of an external class, that's fine, but you must define what the expectations, or Promises, are. Which method should it call? What arguments should it provide? What will it return? After defining this relationship, you have a really clear idea of what's happening.

4. *It speeds up development.* The steps of Red, Green, Refactor can save you hundreds of hours of scratching your head, wondering why what you coded 2 hours ago doesn't align with your expectations. phpspec also has a bunch of awesome code generation features built in. So when you run a test for a class that doesn't exist yet, it offers to create it for you. It also does the same for methods that don't exist. Generating code like this saves you even more time.

5. *It makes your workflow much more efficient.* Point 4 already touched on this, but it makes you a more efficient coder. Because you're continually prompted to think about the behaviour of your code, you'll never go on autopilot and end up writing hundreds of lines of boilerplate code.

6. *It makes coding and testing super fun.* It genuinely does!

7. *It results in tests that are more readable and akin to documentation.* You're encouraged to use whole sentences as test names - making your tests easy to understand and more like documentation than phpunit assertions (think RSpec).
