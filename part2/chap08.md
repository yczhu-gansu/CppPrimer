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

## The IO Classes
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
