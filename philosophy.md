# Programming Philosophy

_“Chaos is merely order waiting to be deciphered.” ― José Saramago, The Double_

As living beings, we make sense of the world by recognizing and reacting to patterns. As programmers, we take those patterns and sort them, filter them, and figure out how to write rules that describe them. Naturally, there is overlap with how we perceive the world, and how we break our tasks down at work. Each of us holds dear a set of 'truths' upon which we base all the logical conclusions in our lives. This is how, even though two people may have perfect logic, they can start from the same place and arrive at different conclusions; the truths they used to interpret the problem were different. This is part of the challenge, and often the joy, of working on a team with other programmers. In many ways a pull request is as much a philosophical exchange as a functional change to a program.

In this section I'll go over a couple of my most essential 'truths', and though there are many more subtle and specific ones that have to do with the kinds of programs I write, these basic ones should apply to any kind of program, and in my opinion, most of life itself.

## Why?
Want to weed a garden? Pull the undesirable plants out and make sure you get the roots, or they will come back. Want to fix a problem in your program? Find the place where the problem originates and do your work there. If you find yourself having to write or change more than a couple of lines of code, it's likely that you haven't yet dug in far enough, and are still compensating for an underlying issue. Ask `Why does this happen?` to dig in until you feel confident that you are looking a the root cause.

Practically speaking, whenever there's a problem, find the easiest place you can think of where you can see it in action, and start working your way back from there. Something appearing incorrect on the screen? Set a breakpoint in the UI, figure out where the data is coming from, how it's calculated or where it's stored. Keep following the thread until you reach a value that you think is actually correct, and between there and the first place where it appears incorrect is probably where you'll need to make a change.

Don't forget, the root cause isn't necessarily just the content of some code, it could be how the concept is abstracted, or even the architecture itself. If the latter is the case, you may in fact need to write more than a couple lines of code, but in the end you should wind up with something much simpler than what you started with. Which brings us to the next point.

## KISS
You've probably heard of this one, most likely before you learned how to program even. Keep It Simple, Stupid. Combined with the DRY principle, you have almost all you need to write some decent and maintainable code.

As holds true with nature, programming should be done with the bare minimum to accomplish your task. The more you do now, the more you will have to re-write and refactor when the product requirements change, be it from external forces or just natural evolution of the OS the program runs on.

If you find that you're having to write a lot of code to satisfy a requirement, it could very well be that the thing you're writing is complicated, but it could also mean that the way you're splitting the problem up doesn't align with what the logic needs to do. Don't be afraid to scrap the whole lot and start over, cut it from a different angle and see where you end up.

Don't forget you have a different lens than everyone around you, and if you get stuck, ask for help, see if one of your colleagues would approach it in a way you haven't thought of yet.

#### Build to the requirements.
Sometimes you get to invent requirements for yourself. There are no two tasks exactly alike and while someone is over here getting perfectly defined Jira tasks (not likely) with badass AC and nice pictures, you may get those fun one liners that say "make it work," and leave the rest to you. Both are totally fine, if everyone involved is used to working that way and understands what the hell is going on. But either way, it's important to understand what is actually being asked of you, and to not go beyond that. At least not without a conversation with whoever wrote the requirements.

While it is important to have the ability to think into the future and see some of the ways the code you write could potentially be used, it's more important to write only what you actually need now. The guesses you are making about what is going to happen are almost certainly going to be wrong in some way, and making modifications to a simple system is always preferable to correcting some complex system that might already have other things tied to it's functionality.

#### Chunk it up.
Logical separation is hard to define when it's too little or too much, but as a general rule of thumb, if you're starting to get into things like nested logic or multi dimensional arrays, it might be time to think about breaking some of the functionality into another structure that makes the code both easier to read and easier to work on. Future you (and everyone else) will thank you for keeping things short and sweet when it's time to go back and understand how some code works and modify it.

Keeping the bits relatively small means that those shifts in direction of the product can potentially have a more granular impact on your code, meaning that you can change sometimes a single class to accommodate a new feature.

A friend once said, "Pretend your new co-worker is an inmate from the local prison with anger management issues and nothing to lose. Write so that they can read it, and you won't get beat."

#### Tech debt.
Tech debt is a term that describes the difference between what was built, and what is needed now. Concepts start to get overloaded, methods take one or two more parameters than is easily readable or usable. Things aren't as DRY or KISSed as we'd like them to be, and it's making us nervous. Ideally there is enough test coverage that we can be confident that things aren't broken yet, but if we let the tech debt go on unchecked, we will soon have a smoldering pile of code that no one wants to touch anymore. It's important to refactor things as we go to fit the new shape of the world we're creating.

## DRY
This is an easy one, but important. It stands for Don't Repeat Yourself, and you've almost certainly already heard about it. Find yourself needing the same bit of code in a couple places? Great, time to break it into a location that is accessible from both places. If you have the same code in two places, and later someone comes back and changes one of them without knowing of the other, your code isn't going to behave the way you think it should. Of course, your tests will catch that anyway, right? Common examples of things that usually need to be in their own shared space are networking classes, UI elements, or database interfaces.

This principle can also be applied to chunks of code that share many commonalities, though they may not be identical. The places where the bits of code differ should become the parameters that are passed into the new method that encapsulates the shared bits.

## Comments
Comments should answer the question _Why is this the way it is?_ If you find yourself having to describe _what_ a piece of code is, that's a potential red flag that the code hasn't been written using the principles described above. What it is should be easily deciphered just by reading it. Naming is one of the more difficult parts of programming, and done right can make reading some code like reading prose, with its purpose and function so painfully obvious that if you read it out loud a five year old could grasp it.

The _why_ is important so that whoever works on this code in the future can have the right concerns in mind when they change things around. As much as possible the why should also be embodied in whatever tests you write.

## Put it together
At the end of the day, what we do is we build tools. It's harder to see because the tools can have any shape we want them to, and there are no (or few) physical limitations on the shapes those tools can have. If we were making tools for a kitchen, we'd want to be making cutting boards, rolling pins, eating utensils and knives. Sure it'd be fun to make a garlic slicer, and an onion slicer, and an eggplant slicer, etc., but if we start down that route, it soon becomes apparent that we'll need a bigger kitchen if we're going to house all the slicers for the different foods we want to cut up. Oh, and that means we'll also need some sort of organization method, perhaps a shelving system with names, as well instructions on how to perform searches on the names and map the results to a location, and instructions for the use of each tool. Maybe even some slicers that cut different thicknesses or shapes for the same foods. Do you see where this is headed? Madness. Find the commonality (DRY), in this case the slicer, and split it out into its own thing, a knife, and leave it at that. Now all you have to do is describe a couple of techniques for getting the shapes you want out of _any_ food, irrespective of what that food turns out to be. You're done, until that requirement for the potato peeler comes in.

Seeing the difference between a big bunch of slicers and a knife when you're programming abstract concepts can be really difficult or subtle, but as long as you are constantly trying to write small, clear code, you can hopefully avoid the trap of having a code base that just seems to keep expanding.

Technology is a problem. Every time we build something, we are most likely making more issues for ourselves to solve. Sorting algorithms for vegetable slicers when all we needed was a single knife. Sure, writing a sorting algorithm is neat and fun, but remember to take a step back from the task and look at the shape of the problem, and see how it matches up to the solution. Keep in mind the nearest exit may be behind you.
