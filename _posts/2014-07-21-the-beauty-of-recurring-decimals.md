---
title: "The beauty of recurring decimals"
layout: post
date: 2014-07-21 00:16:15 CEST
published: true
mathjax: true
categories: mathematics
tags: mathematics
---

One of the coolest parts about a geometric series is the ability to rationalize and control patterns that emerge from it. Althought these recurring patterns can often seem arbitrary, they can actually be represented in a concise way using basic formulae of geometric series.

For example, the pattern $$0.\dot{5}\dot{0}$$. Without the dot notation, this works out to be $$0.5050505050$$ ad infinitum, which is annoying when we need a form to work with. How can we express this recurring decimal in a fraction? Well, when we think about it, a recurring decimal is just a geometric series:

$$
0.505050 = 0.50 + 0.0050 + 0.000050 + ...
$$

Each term is related to its predecessor by a common ratio, $$r$$. To find this ratio, we divide a term by its predecessor:

$$
r = \frac{0.0050}{0.50} = \frac{1}{100}
$$

As the series progresses, the next term is equated by dividing the current term by 100. We know that the first term, $$a$$, is 0.50. To find the total sum of a geometric series to $$n$$ terms:

$$
S_n = \frac{a(1 - r^n)}{(1 - r)}
$$

But we want to find the sum of the series to an infinite amount of terms. How do we do this?

We say that $$S_n$$ tends towards a limiting value as $$n$$ approaches infinity. So, in our case, each term will approximate to zero for large values of $$n$$, i.e. $$\frac{n}{100} \to 0$$ as $$n \to \infty$$. Thus:

$$
S_n = \frac{a(1)}{1-r} \text{as n} \to \infty
$$

Which works out as:
<div>
$$
S_{\infty} = \frac{a}{(1 - r)}$$
</div>
However, $$S_{\infty}$$ only exists for infinite geometric series in which $$|r| < 1$$. This is called a convergent series. So when we apply this equation to our number:

$$S_{\infty} = \frac{\frac{1}{2}}{\frac{99}{100}}
      = \frac{100}{198}
      = \frac{50}{99}
$$

Cool! The recurring decimal $$0.505050$$ can also be represented as $$\frac{50}{99}$$.

Let's try another: $$0.\dot{3}6\dot{0}$$ ($$0.360360360$$):

$$0.360360360 = 0.360 + 0.000360 + 0.000000360$$

$$r = \frac{0.000360}{0.360} = \frac{1}{1000}$$

$$S_{\infty} = \frac{\frac{36}{100}}{\frac{999}{1000}} = \frac{36000}{99900} = \frac{40}{111}$$

Awesome!
