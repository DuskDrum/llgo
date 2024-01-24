# llgo

**This project has moved to llvm.org. Any contributions or bug reports should be sent there. Please refer to the [llgo readme](http://llvm.org/svn/llvm-project/llgo/trunk/README.TXT) for more information.**

llgo is a [Go](http://golang.org) frontend for [LLVM](http://llvm.org), written in Go.

llgo is under active development. It compiles and passes most of the standard library test suite and a substantial portion of the gc test suite, but there are some corner cases that are known not to be handled correctly yet. Nevertheless it can compile modestly substantial programs (including itself; it is self hosting on x86-64 Linux).

Progress will be reported on the [mailing list](https://groups.google.com/d/forum/llgo-dev).

# Installation

llgo requires:
* Go 1.3 or later.
* [CMake](http://cmake.org/) 2.8.8 or later (to build LLVM).
* A [modern C++ toolchain](http://llvm.org/docs/GettingStarted.html#getting-a-modern-host-c-toolchain) (to build LLVM).

Note that Ubuntu Precise is one Linux distribution which does not package a sufficiently new CMake or C++ toolchain.

If you built a newer GCC following the linked instructions above, you will need to set the following environment variables before proceeding:

    export PATH=/path/to/gcc-inst/bin:$PATH
    export LD_LIBRARY_PATH=/path/to/gcc-inst/lib64:$LD_LIBRARY_PATH
    export CC=`which gcc`
    export CXX=`which g++`
    export LIBGO_CFLAGS=--gcc-toolchain=/path/to/gcc-inst

To build and install llgo:

    # Ensure $GOPATH is set.
    go get -d github.com/go-llvm/llgo/cmd/gllgo
    $GOPATH/src/llvm.org/llvm/bindings/go/build.sh -DCMAKE_BUILD_TYPE=Release -DLLVM_TARGETS_TO_BUILD=host
    cd $GOPATH/src/github.com/go-llvm/llgo
    make install prefix=/path/to/prefix j=N  # where N is the number of cores on your machine.

# Running

We install two binaries to `$prefix/bin`: `llgo` and `llgo-go`.

`llgo` is the compiler binary. It has a command line interface that is intended to be compatible to a large extent with `gccgo`.

`llgo-go` is a command line wrapper for `go`. It works like the regular `go` command except that it uses llgo to build.



LLVM（Low Level Virtual Machine）是一个开源的编译器基础设施项目，它提供了一组用于构建编译器和相关工具的库。LLVM 最初设计用于支持C语言的编译，但现在已经演变成一个通用的编译器基础设施，支持多种编程语言。
以下是 LLVM 的主要特性和组件：
1. 前端 (Frontend): LLVM支持多种编程语言的前端，包括C、C++、Objective-C、Swift、Rust等。这些前端负责将源代码转换为中间表示（Intermediate Representation，IR）。
2. 中间表示 (Intermediate Representation，IR): LLVM定义了一种通用的、低级别的中间表示，称为LLVM IR。这是一种抽象的、与平台无关的表示形式，允许在不同阶段进行优化和分析。
3. 优化器 (Optimizer): LLVM包含强大的优化器，可以在中间表示上进行多种优化，以提高程序性能。
4. 后端 (Backend): LLVM的后端将LLVM IR转换为目标平台的机器码。它支持多种目标体系结构，例如x86、ARM、MIPS等。
5. JIT编译器 (Just-In-Time Compiler): LLVM可以用作JIT编译器，使得在运行时将中间表示编译为本地机器码，从而提高程序的执行速度。
6. 工具链 (Toolchain): LLVM提供了一整套构建工具链，包括编译器、汇编器、链接器等。
7. LLVM 的灵活性和通用性使其成为许多编程语言和项目的首选编译器基础设施。许多编程语言（例如Rust、Swift）以及一些知名项目（例如Clang编译器、LLDB调试器）都采用了 LLVM。
