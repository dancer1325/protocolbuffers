# Protocol Buffers - Code Example

* example code / uses Protocol Buffers -- to manage an -- address book
  * 2 programs / supported language
    * "add_person"
      * adds a new person | address book / prompt the user -- to -- input the person's information
    * "list_people"
      * lists people ALREADY | address book
      * SAME format | ALL 3 languages
        * -> _Example:_ you can use "add_person_java" to create an address book & use "list_people_python" to read it
* check guide | https://developers.google.com/protocol-buffers/docs/tutorials

## Build the example using bazel

* requirements
  * bazel v0.5.4+
* steps
  * [download/install it](https://github.com/bazelbuild/bazel/releases)
  * `bazel build :all`
    * build the code
  * `bazel-bin/add_person_cpp addressbook.data`
    * run the built binary
* how to use protobuf | your own bazel project
  * [BUILD.bazel](BUILD.bazel)
  * [WORKSPACE](WORKSPACE)

## Build the example using make

* requirements
  * install
    * protocol compiler (i.e., the protoc binary)
    * protobuf runtime / language you want to build
* `make`
  * build the example / ALL languages -- EXCEPT for Go
  * it will likely fail
    * Reason: 🧠different languages have different installation requirements 🧠
* if you want to build ONLY | specific language -> follow individual instructions below

### C++

You can follow instructions in [../src/README.md](../src/README.md) to install
protoc from source.

Then run "make cpp" in this examples directory to build the C++ example. It
will create two executables: add_person_cpp and list_people_cpp. These programs
simply take an address book file as their parameter. The add_person_cpp
programs will create the file if it doesn't already exist.

To run the examples:

    $ ./add_person_cpp addressbook.data
    $ ./list_people_cpp addressbook.data

Note that on some platforms you may have to edit the Makefile and remove
"-lpthread" from the linker commands (perhaps replacing it with something else).
We didn't do this automatically because we wanted to keep the example simple.

### Python

Follow instructions in [../README.md](../README.md) to install protoc and then
follow [../python/README.md](../python/README.md) to install protobuf python
runtime from source. You can also install python runtime using pip:

    $ pip install protobuf

Make sure the runtime version is the same as protoc binary, or it may not work.

After you have install both protoc and python runtime, run "make python" to
build two executables (shell scripts actually): add_person_python and
list_people_python. They work the same way as the C++ executables.

### Java

* [../README.md](../README.md) -- to install -- protoc
* download protobuf Java runtime .jar
  * https://mvnrepository.com/artifact/com.google.protobuf/protobuf-java
*    
    ```
    export CLASSPATH=/path/to/protobuf-java-[version].jar
    make java
    ```
  * -> will be created add_person_java/list_people_java executables

### Go

Follow instructions in [../README.md](../README.md) to install protoc. Then
install the Go protoc plugin (protoc-gen-go):

    $ go install google.golang.org/protobuf/cmd/protoc-gen-go@latest

The "go install" command will install protoc-gen-go into the GOBIN
directory.  You can set the $GOBIN environment variable before
running "go install" to change the install location.  Make sure the
install directory is in your shell $PATH.

Build the Go samples with "make go".  This creates the following
executable files in the current directory:

    add_person_go      list_people_go

To run the example:

    ./add_person_go addressbook.data

to add a person to the protocol buffer encoded file addressbook.data.  The file
is created if it does not exist.  To view the data, run:

    ./list_people_go addressbook.data

Observe that the C++, Python, Java, and Dart examples in this directory run in a
similar way and can view/modify files created by the Go example and vice
versa.

### Dart

First, follow the instructions in [../README.md](../README.md) to install the Protocol Buffer Compiler (protoc).

Then, install the Dart Protocol Buffer plugin as described [here](https://github.com/dart-lang/dart-protoc-plugin#how-to-build-and-use).
Note, the executable `bin/protoc-gen-dart` must be in your `PATH` for `protoc` to find it.

Build the Dart samples in this directory with `make dart`.

To run the examples:

```sh
$ dart add_person.dart addressbook.data
$ dart list_people.dart addressbook.data
```

The two programs take a protocol buffer encoded file as their parameter.
The first can be used to add a person to the file. The file is created
if it does not exist. The second displays the data in the file.
