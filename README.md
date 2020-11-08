# CppPrimer
Learning *C++ Primer*

## Part 2 The C++ Library
With each revision of the C++ language, the library has also grown. There are
core facilities that the library defines that every C++ programmer should be
comfortable using.

Central to the library are a number of container classes and a family of generic
algorithms that let us write programs that are succinct and efficient. The
library worries about bookkeeping details -- in particular, taking care of
memory management -- so that our programs can worry about the actual problems we
need to solve.

The algorithms typically operate on a range of elements in a sequential
container or other sequence. The algorithms library offers efficient
implementation of various classical algorithms, such sorting and searching, and
other common tasks as well. The algorithms generic in two ways: They can be
applied to different kinds of sequences, and those sequences may contain
elements of most types.

The library also provides several associative containers. Elements in an
associative container are accessed by key. The associative containers share many
operations with the sequential containers and also define operations that are
specific to the associative containers.

Language and library facilities for managing dynamic memory. One of the most
important new library classes, which are standardized versions of smart
pointers. By using smart pointers, we can make code that uses dynamic memory
much more robust.
8. [The IO Library](./part2/chap08.md)
