# 8. The IO Library
In the C++ language, iO is handled by a family of types defined in the
standard library. These types support IO to and from devices such as
files and console windows. Additional types allow in-memory IO to and from
*strings*.

The IO library defines operations to read and write values of the built-in
types. In addition, classes, such as *string*, typically define similar IO
operations to work on objects of their class type as well.

IO library facilities:
1. *istream* (input stream) type, which provides input operations
2. *ostream* (output stream) type, which provides output operations
3. *cin*, an *istream* object that reads the standard input
4. *cout*, an *ostream* object that writes to the standard output
5. *cerr*, an *ostream* object, typically used for program error messages, that
   writes to the standard error
6. The *>>* operator, which is used to read input from an *istream* object
7. The *<<* operator, which is used to write output to an *ostream* object
8. Ghe *getline()* function, which reads a line of input from a given *istream*
   into a given *string*

## 8.1 The IO Classes
The different kinds of IO processing:
1. Connect to the user's console window, and manipulate *char* data;
2. Read or write named files;
3. Use IO operations to process the characters in a string;
4. Read and write languages that require wide-character support.

The library defines a collection of types. These types are defined in three
separate **headers**:
* *iostream*, defines the basic types used to read from and write to a stream.
* *fstream*, defines the types used to read and write named files.
* *sstream*, defines the types used to read and write in-memory strings.

IO Library Types and Headers
| **Header** | **Type** |
| --- | --- |
| iostream | *istream, wistream* reads from a stream<br>*ostream,wostream* writes to a stream<br>*iostream,wiostream* reads and writes a stream |
| fstream| *ifstream,wifstream* reads from a file<br>*ofstream,wofstream* writes to a file<br>*fstream,wfstream* reads and writes a file |
| sstream | *istringstream,wistringstream* reads from a string<br>*ostringstream,wostringstream* writes to a string<br>*stringstream,wstringstream* reads and writes a string |

A set of types and objects that manipulate *wchar_t* data. For example, wcin,
wcout, and wceer are the wide-character objects.

The wide-character types and objects are defined in the same headers as the
plain char types. For example, the *fstream* header defines both the *ifstream*
and *wifstream* types.

#### Relationship among the IO types
Conceptually, neither the kind of device nor the character size affects the IO
operations we want to perform.

The library lets us ignore the differences among these different kind of streams
by using **inheritance**. As with templates, we can use classes related by
inheritance without understanding the details of how inheritance works.

Inheritance lets us say that a particular class inherits from another
class. We can use an object of an inherited class as if it were an object of the
same type as the class from which it inherits.

The types *ifstream* and *istringstream* inherit from *istream*.

### 8.1.1 No copy or Assign for IO Objects
We cannot copy or assign objects of the IO types:
```C++
ofstream out1, out2;
out1 = out2;				// error: cannot assign stream objects
ofstream print(ofstream);	// error: can't initialize the ofstream parameter
out = print(out2);			// error: can't copy stream objects
```
Because we can't copy the IO types, we cannot have a parameter or return type
that is one of the stream types. Functions that do IO typically pass and return
the stream through references. Reading or writing an IO object changes its
state, so the reference must not be *const*.

### 8.1.2 Condition States
Inherent in doing IO is the fact that errors can occur. Some errors are
recoverable, others occur deep within the system and are beyond the scope of a
program to correct.

The IO classes define functions and flags, that let us access and manipulate the
**condition state** of a stream.

Because a stream might be in an error state, code ordinarily should check
whether a stream is okay before attempting to use it. The easiest way to
determine the state of a stream is to use that object as a condition:
```C++
while (cin >> word)
	// ok: read operation successufl ...
```
Check the state of the stream returned from the >> expression.

#### Interrogating the State of a Stream
Sometimes we need to know why the stream is invalid. 

The IO library defines a machine-dependent integral type named *iostate* that it
uses to convey information about the state of a stream. The IO classes define
four *constexpr* values of type *iostate* that represent particular bit
patterns. These values are used to indicate particular kinds of IO conditions.
They can be used to indicate particular kinds of IO conditions. They can be used
with the bitwise operators to test or set multiple flags in one operation.
* *badbit*, indicates a system-level failure. It is usually not possible to use
  a stream once *badbit* has been set.
* *failbit*, a recoverable error. It is possible to continuing using the stream.
* *eofbit, failbit*, reading end-of-file, sets both those bits.
* *goodbit*, have value 0, indicates no failures on the stream.

If any of *badbit, failbit, eofbit* are set, the a condition that evaluates that
stream will fail.

The library also defines a set of functions to interrogate the state of these
flags.

Table: IO Library Condition State
| **State/Function** | **Description** |
| --- | --- |
| strm::iostate | strm is one of the IO types. iostate is a machine-dependent integral type that represents the condition state of a stream. |
| strm::badbit | strm::iostate value used to indicate that a stream is corrupted. |
| strm::failbit | strm::iostate value used to indicate that an IO opperation failed. |
| strm::eofbit | strm::iostate value used to indicate that a stream hit end-of-file. |
| strm::goodbit | strm::iostate value used to indicate that a stream is not in an error state. This value is guaranteed to be zero. |
| s.eof() | true if eofbit in the stream s is set. |
| s.fail() | true if failbit or badbit in the stream s is set. |
| s.bad() | true if badbit in the stream s is set. |
| s.good() | true if the stream s is in a valid state. |
| s.clear() | Reset all condition values in the stream s to valid state.  Returns void.|
| s.clear(flags) | Reset the condition of s to flags. Type of flags is strm::iostate. Returns void. |
| s.setstate(flags) | Adds specified conditions(s) to s. Type of flags is strm::iostate. Returns void. |
| s.rdstate() | Returns current condition of s as a strm::iostate value. |

#### Managing the Condition State

