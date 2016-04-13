# Mark & Sweep Garbage Collection

## Mark Phase

### Concepts

* Block Colours (black, white, grey)
* References
* GC Root (frames, global variables)

Repeat the following process:

a) For each white block.
b) Visit all white references, mark them as grey.
c) Mark the white block from a) as Black.


## Sweep Phase

Finally find black blocks with no references.

## Generations


### Concepts

* One of the jobs of the garbage collector is seperate the heap into more than one generations.
* Generational Hypothesis (most objects die young)
* Nursey (Where small objects are born)
  * Nursey has a fixed size, allocations are very efficient and once it fills up the nursey is collected.

* Major (Where they are copied to when they mature)
* Large Object Space (Part of major, objects above Kb, typically large arrays)

## Videos

* https://www.youtube.com/watch?v=VJsmrTQWD2k

## Reading Materials
* https://www.quora.com/What-is-the-generational-hypothesis-in-the-context-of-garbage-collection
* http://www.brpreiss.com/books/opus5/html/page424.html
* http://c2.com/cgi/wiki?MarkAndSweep
