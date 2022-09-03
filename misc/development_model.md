# Intuitive development model

*Updated 2022-06-22*

Current development models are ... kind of odd. I would like to discuss an intuitive development model.

## The "natrual" way of developing software

I think to make a good development model, we need to figure out how we would intuitively work on a project both for ourselves and with other people.

> **Note**: Of course, any idea of "natrual" would be idealised and at least partially impractical, but it would also be intuitive and ... natrual, so it makes sense that you should want to take advantage of the nice parts of something having little overhead and being able to be done easily.

### What?

It seems common for people to start by wanting to accomplish *something*. The end goal doesn't need to be concrete or centered in reality: think about pure mathematics, doing things for the sake of doing them.

So, the first thing that should probably go into this pipeline is establishing some kind of task that should be completed. That can be in the form of an issue or an entire project, but (pretty obviously), you need to know the thing that you want to do.

> **Tip**: If you're trying to solve an issue, make sure to keep focused on solving that issue (and any other issues that could need solving as a prerequsite). If you are building something larger, make sure to stay focused on a small but easily extendable product.

### How? The Learning (and fun) Part

After that, it seems reasonable to want to think about how you will go about doing that thing and consider what you have to work with in more detail.

This includes choosing a specific solution to the problem if this problem is more general, doing any form of engineering work and thinking through the problem in a way that is easy to understand.

You might also want to think about any corner cases, expriment with different possible ways of doing things, touch on any part of your solution you might be unfimiliar with and generally make sure you understand what you are doing before you try to do things seriously. (It's good to be prepared!)

> **Note**: Most of the problem solving and learning of programming should be here, and this is probably the part that you should spend the most time on. If you don't understand your work, then something is wrong.

> **Tip**: If you are making a new API, you might write sample code or specify an example interface. This makes sure that you will enjoy using your API and that others will too. 

### Commiting and implementing things

After you've really done the heavy lifting of figuring out how to make this work, it's probably most natrual to want to see the results of your work. This is the time to implement, test and debug! If any unanticipated issues come up, this is also the time to visit those and make sure that what you are doing is well polished.

### Finalising the work

Finalising the work you have done includes the process of merging your work into the mainline branch and making the final checks to make sure the work you have done will work and be maintainable.

## Formalising the routine

> **Note**: This is not a completed section.

### Time

The first thing you might notice is that this model doesn't really specify timeframes for things, nor does it try to limit who can do what or exactly how things get done. Good software - like, *actually good software* - takes *a lot of time*.

And truthfully, very little of that time is really spent programming! Most of the time, software developers are learning about how to do things and solve problems - even ones that they might be unfimilar with. And as we know, it's usually not good to force learning into a small timeframe - that leads to a lot of bullshit.

So, a good software project will take time.

> **Note**: My personal analogy is that this model is like mastery based learning for software: we require ourselves to make good software, and we let the time we have to do it slide around.

> **Note**: Perhaps there is the argument to be made that time is money and more money is good. First, if you really like money so much, you're an arsehole. (F\*ck you!) But also, it should be pointed out that when you give the right people and give them a more flexible schedule, some can make more progress by working slowly initially rather than quickly working and spending forever fixing any bugs.

## Comparing to other development models

### Agile

From the [website](https://agilemanifesto.org/iso/en/manifesto.html):

> We are uncovering better ways of developing software by doing it and helping others do it. Through this work we have come to value:
> 
> * **Individuals and interactions** over processes and tools
> * **Working software** over comprehensive documentation
> * **Customer collaboration over** contract negotiation
> * **Responding to change over** following a plan
> 
> That is, while there is value in the items on the right, we value the items on the left more.

I can understand where they come from; however, I think that beliving you should normally prioritise one thing over the other is kind of a trap.