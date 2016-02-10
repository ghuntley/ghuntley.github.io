# Topic

Imperative Programming is Dangerous

# Abstract

When we rely on hoping that the behavior that emerges from a program is correct, 
and that reliance is based on nothing more than a programmer's correctness, then
we can easily find ourselves in a sticky situation. We can try and mitigate the
costs of imperative programming with things like unit tests or integration tests,
but why mitigate the costs when there's a better way?

# Audience level

# Structure

## History of Computing

## The 1980's: A Revolution in Software

## Imperative Programming is Dangerous

## There is a Better Way

## Functional Reactive Programming

Functional. Reactive. Programming. What on Earth is that?

Well, we know to some degree what functional programming is. Functions don't have side-effects; there's no mutable state. It's a difficult way to program since the real world is mutable. Modeling things like user input becomes a nightmare.

Reactive programming? What's that? Well, the best way to describe reactive programming is to think of a spreadsheet. 

### Signals
* Everyone says Functional Reactive Programming is hard, but anyone who writes Excel expression is doing it

Imagine three cells, A, B, and C. A is defined as the sum of B and C. Whenever B or C changes, A reacts to update itself. That's reactive programming: changes propagate throughout a system automatically.

Functional reactive programming is just a combination of functional and reactive paradigms. We model user input as a function that changes over time, abstracting away the idea of mutable state.

## Code
* ReactiveCommand and OpenBrowser
 
## Conclusion
Instead of telling a computer how to do its job, why don't we just tell it what it's job is and let it figure the rest out? The bottom line is imperative programming is error-prone and relies too heavily on the infallibility of the programmer.

Functional reactive programming is the peanut butter and chocolate of programming paradigms.
