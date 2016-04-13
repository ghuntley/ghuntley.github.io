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

# Generations

## Videos

* https://www.youtube.com/watch?v=VJsmrTQWD2k

## Reading Materials
* http://www.brpreiss.com/books/opus5/html/page424.html
* http://c2.com/cgi/wiki?MarkAndSweep
