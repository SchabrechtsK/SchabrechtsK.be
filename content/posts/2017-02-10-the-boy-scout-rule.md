---
title: The Boy Scout Rule
author: Kenneth
type: post
date: 2017-02-10T00:00:00+00:00
url: /development/the-boy-scout-rule/
featured_image: /wp-content/uploads/2017/02/1D18D6IY40HmcCkGvAHQhVA.jpeg
categories:
  - Development
tags: []

---
<p id="60ea" class="graf graf--p graf-after--figure">
  A few weeks back I was at another great edition of the PHPBenelux Conference. And one of the topics that always has a speaker is the one about legacy code. It is just something most of us have to deal with.
</p>

<p id="dcdb" class="graf graf--p graf-after--p">
  It was during the last evening social. I was talking with a few great developers about the problem of legacy code. One of them mentioned the Boy Scout rule. Which seemed like a very useful rule.
</p>

<p id="cefc" class="graf graf--p graf-after--p">
  Those who work with legacy code know that most of the time these projects can be a source of agony. Most of the time they’re build with the wrong expectations. The developers might not had the business knowledge they needed to create a decent code base. Or it is one hack after another.
</p>

<p id="87ab" class="graf graf--p graf-after--p">
  The most preferred way to work with these types of project is to just start over from scratch. Unfortunately this is not always a viable option. In comes the Boy Scout Rule:
</p>

<blockquote id="836b" class="graf graf--pullquote graf-after--p">
  <p>
    Always leave the campground cleaner than you found&nbsp;it.
  </p>
</blockquote>

<p id="5cb6" class="graf graf--p graf-after--pullquote">
  Now, this is one rule we can easily interpret as the following for code:
</p>

<blockquote id="cfae" class="graf graf--pullquote graf-after--p">
  <p>
    Always check a module in cleaner than when you checked it&nbsp;out.
  </p>
</blockquote>

<p id="2aba" class="graf graf--p graf-after--pullquote">
  Imagine that you are working on this kind of project. You check-out the code and do the change needed. Next you make sure the test pass. The documentation gets written and you make a pull request. You no longer look at the rest of the code.
</p>

<p id="d1fe" class="graf graf--p graf-after--p">
  But what if instead you go the extra mile? It can be as simple as adding missing documentation. You can change variables to something more readable. Heck, You can even go further and split a long function in two smaller functions. Or why not add missing interfaces. And even break circular dependency.
</p>

<p id="2f1f" class="graf graf--p graf-after--p">
  That one extra mile would improve the code with each change made. And the project would get better and better as it evolves.
</p>

<p id="5163" class="graf graf--p graf-after--p">
  And it’s not only about improving the code. The entire projects code becomes a team effort. No longer is everyone only working on their piece of the puzzle as I’ve seen so often.
</p>

<p id="8d16" class="graf graf--p graf-after--p">
  And it’s not only for legacy code, it also works for new projects. There are always pieces of code that need improvement. Knowledge that you should pass upon the rest of the team through the code.
</p>

<p id="fac3" class="graf graf--p graf-after--p graf--trailing">
  Consider using the Boy Scout rule and have a cleaner code base.
</p>