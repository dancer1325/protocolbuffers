Protocol Buffers - Google's data interchange format
===================================================

Copyright 2008 Google Inc.

https://developers.google.com/protocol-buffers/

CMake Installation
-----------------------

* check [cmake/README.md](../cmake/README.md)

C++ Protobuf - Unix
-----------------------

* goal
  * build protobuf -- from -- source
* steps
  * install the following tools: bazel, git, g++, Abseil
    * `sudo apt-get install g++ git bazel`  | Ubuntu
    * check
      * https://bazel.build/install
      * [cmake/README.md](../cmake/README.md)
        * build from source -- via -- CMake
      * https://github.com/abseil/abseil-cpp
  * get the source code
    * download the release .tar.gz or .zip package in https://github.com/protocolbuffers/protobuf/releases/latest
    * get it from https://github.com/protocolbuffers/protobuf.git 
      ```
      git clone https://github.com/protocolbuffers/protobuf.git
      cd protobuf
      git submodule update --init --recursive  // check if the submodules have been ALSO cloned
      ```
  * `bazel build :protoc :protobuf`
    * build the 
      * C++ Protocol Buffer runtime &
      * Protocol Buffer compiler -- `protoc`
  * copy the generated `protoc` -- to -- /usr/local/bin 
    * _Example:_ on Linux
      ```
      cp bazel-bin/protoc /usr/local/bin    
      ```
  * `protoc --version`
    * check it's installed

**Compiling dependent packages**

* if you want to compile a package / uses Protocol Buffers -> set up a Bazel WORKSPACE /
  * -- hooked up to the -- protobuf repository
  * loads its dependencies
* _Example:_ [WORKSPACE](../examples/WORKSPACE)

**Note for Mac users**

* Unix tools are NOT available by default | Mac
* steps
  * install Xcode -- from the -- Mac AppStore
  * `sudo xcode-select --install`
  * install bazel
    * `sudo /opt/local/bin/port install bazel`
      * https://www.macports.org
      * allowed for MOST Mac installations
    * `brew install bazel`
  * follow the Unix instructions above

C++ Protobuf - Windows
--------------------------

If you only need the protoc binary, you can download it from the release
page:

    https://github.com/protocolbuffers/protobuf/releases/latest

In the downloads section, download the zip file protoc-$VERSION-win32.zip.
It contains the protoc binary as well as public proto files of protobuf
library.

Protobuf and its dependencies can be installed directly by using `vcpkg`:

    >vcpkg install protobuf protobuf:x64-windows

If zlib support is desired, you'll also need to install the zlib feature:

    >vcpkg install protobuf[zlib] protobuf[zlib]:x64-windows

See https://github.com/Microsoft/vcpkg for more information.

To build from source using Microsoft Visual C++, see [cmake/README.md](../cmake/README.md).

To build from source using Cygwin or MinGW, follow the Unix installation
instructions, above.

Binary Compatibility Warning
----------------------------

* unlikely that 2 versions Protocol Buffers C++ runtime libraries / compatible ABIs
  * Reason: 🧠 due to the nature of C++ 🧠
  * == if an executable -- is linked against an -- older version of libprotobuf -> unlikely to work with a newer version
    * -> you need to re-compile
    * `linkstatic=True` | `cc_binary` Bazel rules
  * use cases
    * startup of your app


Usage
-----

* Check https://protobuf.dev/
