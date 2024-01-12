# VE280 2024SP RC1

## Prerequisites

I assume that you have already setup the following environment:

- A working Linux environment (either a VM or a physical machine)
- A working C++ compiler on your Linux or MacOS system

If you haven't done so, please refer to my RC0 for more details.

## Intro to Linux

### File System

In Linux, everything is a file. The file system is a tree structure. The following figure gives a brief demonstration of the file system.

<!-- markdownlint-disable MD033 -->
<p align="center">
  <img src="./LinuxFile.png" alt="Linux File System" width="66%">
</p>
<!-- markdownlint-enable MD033 -->

Key points:

- `/` is the root directory
- `.` is the current directory
- `..` is the parent directory
- `~` is the home directory

### Command Line Interface

In linux (and MacOS), we can use **C**ommand **L**ine **I**nterface to interact with a computer. It is fast, easy to automate and easy to use remotely. By default your terminal has a shell named `bash`.

The general syntax of a command is:

```bash
command [options] [arguments] # or
command arg1 arg2 ...
```

#### Basic Commands

- `man <command>`: read the manual of a command
  - this command can be replaced by `tldr` in most cases, which I introduced in RC0
- `pwd`: print working directory
- `ls`: list files and directories
  - `ls -a`: list all files and directories including hidden ones
  - `ls -l`: list files and directories in long format

Pay attention to the long format of `ls`:

- The first character indicates the type of the file
  - `-`: regular file
  - `d`: directory
- The next 9 characters indicate the permissions of the file
  - `r`: read
  - `w`: write
  - `x`: execute
  - The first three characters indicate the permissions of the owner
  - The second three characters are for the group
  - The last three characters are for others

<!-- markdownlint-disable MD033 -->
<p align="center">
  <img src="./longls.png" alt="ls" width="80%">
</p>
<!-- markdownlint-enable-MD033 -->

- `cd`: change directory
  - `cd <path>`: change to the directory specified by `<path>`
  - `cd ..`: change to the parent directory
  - `cd ~`: change to the home directory
- `mkdir <directory>`: make a new directory specified by `<directory>`
- `rmdir <directory>`: remove an empty directory specified by `<directory>`
- `touch <file>`: create an empty file specified by `<file>`
- `rm <file>`: remove a file or directory specified by `<file>`
  - `rm -r <file>`: remove a directory recursively
    **Necessary for removing non-empty folders**
  - `rm -i <file>`: ask for confirmation before removing a file or directory
  - `rm -f <file>`: force remove a file or directory
    **This can be dangerous**
- `cp <source> <destination>`: copy a file or directory from `<source>` to `<destination>`
  - `cp -r <source> <destination>`: copy a directory recursively
    **Necessary for copying non-empty folders**
- `mv`: move a file or directory or rename a file
  - `mv <file1> <file2>`: rename a file or directory from `<file1>` to `<file2>`
  - `mv <file> <directory>`: move a file or directory to a directory
  - `mv <directory> <directory>`: move a directory to another directory
- `cat <file>`: print the content of a file
  - There's a modern version of `cat` called `bat`

#### Advanced Commands

These commands are necessary as well and you may encounter them in exams.

- `less <file>`: view a file with a read-only mode
  - `less` is a pager, which means it only loads a part of the file at a time
  - quit `less` by pressing `q`
  - supports `vim` key bindings, which I introduced in RC0
    **It's really useful to learn `vim` key bindings**
- `diff <file1> <file2>`: compare two files
  - `diff` is a tool to compare two files line by line
  - `diff` is a very useful tool when you want to check the difference between two files, especially when you want to check the difference between your output and the standard output. This is the most useful tool in this course and for your projects, from my perspective.
  - useful options:
    - `-y`: output in two columns
    - `-w`: ignore all white spaces, important when comparing two files with different indentation
  - Also, you may refer to a VSCode extension called `Partial Diff` for a better experience
- `nano`, `gedit`, `vim`, `emacs`: text editors
  - the command `code` can be directly used in shell to launch VSCode
    e.g. `code <file>` or `code <directory>`
- Auto completion
  - press `Tab` to auto complete a command or a file name
  - you may use `zsh-autosuggestions` to enable auto suggestions by pressing `->`, which I introduced in RC0
- `sudo apt-get install <package>`: install a package
  - `sudo` is used to run a command as a super user
  - you may edit read-only files with `sudo`
    e.g. `sudo vim /etc/apt/sources.list` when changing the mirror source of `apt-get`
  - `apt-get` is a package manager, equivalent to `apt`

You may find these commands frustrating at first, but you will get used to them after some practice. Consult the Internet or even ChatGPT, they're good at these detailed questions. For your daily workflow, you may use command line tools like `ranger` or `nnn` to manage files and directories, which does these commands by custom key bindings and is more efficient and convenient than GUI. You may refer to my RC0 for more details.

But make sure you know how to use these commands, as they will be covered in midterm. Don't worry, you'll get to know them after some practice, like in exercise 1.

#### I/O Redirection

In Linux, we can redirect the input and output of a command. The general syntax is:

```bash
command/executable < input > output
# e.g.
cat < input.txt > output.txt
./my_program < input.in > output.out
```

Here the `input` is used as `stdin` of the command/executable and the `output` is used as `stdout` of the command/executable. Note:

- The output redirection will overwrite the file if it exists
- The input redirection will fail if the file does not exist
- The output redirection will create the file if it does not exist
- To append to a file, use `>>` instead of `>`
  e.g. `./my_executable >> output.out` will append the output to `output.out`

This trick is very useful when you want to test your program with some test cases and will be frequently used in your projects. Having a good command of this trick will save you a lot of time.

## Developing and Compiling C++ Programs on Linux

### C++ Compiler: `g++`

For the coding part, you may still use VSCode, but make sure you're using `wsl: Ubuntu` as your environment.

In this course, we will use `g++` as the compiler. I won't explain the process of compilation, and you may refer to the lecture slides for more details. The general syntax of `g++` is:

```bash
g++ [options] <source> -o <executable>
# e.g.
g++ -std=c++17 -Wall -g -o my_executable my_program.cpp
```

Here the `-std=c++17` option specifies the C++ standard to use, the `-Wall` option enables all warnings, the `-g` option enables debugging information and the `-o` option specifies the name of the executable. Note that the order of the options matters. The `-o` option should be placed before the executable name.

#### Caution

**Note that since this course will use C++17, you should always turn on the `-std=c++17` flag.**

### Makefile

For large projects, it's not convenient to compile all the files manually. We can use `make` to automate the process. `make` is a build automation tool that automatically builds executable programs and libraries from source code by reading files called `Makefile`s which specify how to derive the target program.

The general syntax of `make` is:

```makefile
Target: Dependencies
    Command # Don't forget the indentation
```

Below is a simple example of a `Makefile`:

```makefile
all: my_executable

my_executable: my_program.o my_class.o
    g++ -std=c++17 -Wall -g -o my_executable my_program.o my_class.o

my_program.o: my_program.cpp
    g++ -std=c++17 -Wall -g -c my_program.cpp

my_class.o: my_class.cpp
    g++ -std=c++17 -Wall -g -c my_class.cpp

clean:
    rm -f my_executable *.o # Here * is a wildcard
```

You may also write this `Makefile` in a more concise way:

```makefile
CXX = g++
CXXFLAGS = -std=c++17 -Wall -g

all: my_executable

my_executable: my_program.o my_class.o
    $(CXX) $(CXXFLAGS) -o my_executable my_program.o my_class.o

my_program.o: my_program.cpp
    $(CXX) $(CXXFLAGS) -c my_program.cpp

my_class.o: my_class.cpp
    $(CXX) $(CXXFLAGS) -c my_class.cpp

clean:
    rm -f my_executable *.o
```

You may find the compile flag `-c` confusing. It means that the compiler will only compile the source file and generate an object file, which is a file with the extension `.o` and is not executable. These files are called object files and are used to link the program. The linker will link all the object files and generate an executable program. This is a short introduction to the compilation process and the detailed process is not covered in this course.

Here `CXX` is the C++ compiler and `CXXFLAGS` is the flags for the compiler and are stored as variables. Also, note that the indentation is a `tab` character, not spaces.

To run `make`, simply type `make` in the directory where the `Makefile` is located. To clean the directory, type `make clean`. You can customize the `Makefile` to fit your needs and you may refer to the Internet for more details. This is also a very useful tool for your projects.

Also, I've set aliases for some Makefile commands in my `~/.zshrc`, if you're using `bash`, you may add the following lines to your `~/.bashrc`, the syntax is the same:

```bash
alias mkc='make clean'
alias rmk='mkc; make'
```

Then you can simply type `rmk` to recompile your program and `mkc` to clean the directory. Feel free to customize your own aliases!

### Header Files

In our projects, we will handle multiple source files of two types: `.cpp` files and `.h` files. In header files, we will declare the classes and functions and in `.cpp` files, we will define and implement the classes and functions. The general syntax of a header file is:

```cpp
#ifndef MY_HEADER_H // header guards
#define MY_HEADER_H // header guards

// declarations
void my_function(int a, int b);

#endif // header guards
```

and the corresponding `.cpp` file is:

```cpp
#include "my_header.h" // include the declarations
#include <iostream>

// implementations
void my_function(int a, int b) {
    // do something
}
```

then you can use the function `my_function` in other `.cpp` files by including the header file:

```cpp
#include "my_header.h"
// note that you're including the header file here, not the cpp file

int main() {
    my_function(1, 2);
    return 0;
}
```

After that, you can compile and run the program by:

```bash
g++ -o my_executable my_program.cpp my_header.cpp
./my_executable
```

**Question: Why do we need header guards?**

The process of `#include` is replacing the `#include` line with the content of the header file. If we include the same header file multiple times, the compiler will complain about the redefinition of the classes and functions. The header guards are used to prevent this from happening. The following example demonstrates a case where the header guards are necessary:

```cpp
#ifndef MY_HEADER1_H
#define MY_HEADER1_H

// declarations

#endif
```

```cpp
#ifndef MY_HEADER2_H
#define MY_HEADER2_H

#include "my_header1.h"

// declarations

#endif
```

```cpp
#ifndef MY_HEADER3_H
#define MY_HEADER3_H

#include "my_header1.h"
#include "my_header2.h"

// other declarations

#endif
```

Here `my_header1.h` is included in `my_header2.h` and `my_header3.h` and `my_header2.h` is included in `my_header3.h`. If we don't use header guards, the compiler will complain about the redefinition of the contents of `my_header1.h`.

By the way, this question is from the midterm of last semester.

## Exercises

The Linux command part is covered in last semester's midterm, and below are some exercises for you to practice.

1. Under the current directory, create a directory named `VE280`. Assume this directory does not exist.

<pre>
<code style="background-color: #f0f0f0; display: block; padding: 10px;">

</code>
</pre>

2. Create a file named `test.cpp` under the directory `VE280`. Assume this file does not exist and you may want to change your working directory to `VE280` first.

<pre>
<code style="background-color: #f0f0f0; display: block; padding: 10px;">

</code>
</pre>

3. List all files and directories under the current directory in long format including hidden ones.

<pre>
<code style="background-color: #f0f0f0; display: block; padding: 10px;">

</code>
</pre>

4. Compile the file `test.cpp`, `test.h` and `main.cpp` under the directory `VE280` and generate an executable named `test`.

<pre>
<code style="background-color: #f0f0f0; display: block; padding: 10px;">

</code>
</pre>

5. Run the executable `test` and redirect the input from `input.txt` and redirect the output to `output.txt`.

<pre>
<code style="background-color: #f0f0f0; display: block; padding: 10px;">

</code>
</pre>

6. Compare the contents of `output.txt` and `standard.txt` and output the result in `diff.txt`.

<pre>
<code style="background-color: #f0f0f0; display: block; padding: 10px;">

</code>
</pre>

7. Read the content of `diff.txt` in a read-only mode.

<pre>
<code style="background-color: #f0f0f0; display: block; padding: 10px;">

</code>
</pre>

8. Copy the file `test.cpp` to `test2.cpp` under the directory `VE280`.

<pre>
<code style="background-color: #f0f0f0; display: block; padding: 10px;">

</code>
</pre>

9. Rename the file `test2.cpp` to `test3.cpp` under the directory `VE280`.

<pre>
<code style="background-color: #f0f0f0; display: block; padding: 10px;">

</code>
</pre>

10. Change the current directory to the parent directory of `VE280` and remove the directory `VE280` recursively. Remember that it's non-empty.

<pre>
<code style="background-color: #f0f0f0; display: block; padding: 10px;">

</code>
</pre>

## References

[1] Zhanxun Liu. VE280 RC1. 2023FA.

[2] Weikang Qian. VE280 Lecture 2-3.
