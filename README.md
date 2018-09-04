## ncc

C/C++ Naming convention checker (ncc)

ncc is a development tool to help programmers write C/C++ code that adheres to
a some naming conventions. It automates the process of checking C/C++ code to
spare humans of this boring (but important) task. This makes it ideal for
projects that want to enforce a coding standard.

## Status
Work In Progress

## Requirements

* python2
* python-clang
* python-yaml

## Usage

    ncc.py [OPTIONS...] FILE [FILE ...]

For standalone files:

    ncc.py --style=styles/ncc.style examples/test.cpp

For recursing through a directory structure:

    ncc.py --style=styles/ncc.style --recurse examples

For detailed description of all options:

    ncc.py --help

## Style Defintion

Style for c/c++ constructs are defined by regular expresssions. For e.g the below rules say that
a struct can have any character, a class name should begin with 'C', and a class member variable
should begin with m_

    StructName: '^.*$'
    ClassName: '^C.*$'
    ClassMemberVariable: '^m_.*$'
    FunctionName: '^[A-Z].*$'
    Namespace: '^.*$'

## Example Usage

### Check file test.cpp for naming convention violations:

    ./ncc.py --style examples/ncc.style --path examples/test.cpp

    examples/test.cpp:16:7: "B" does not match "^C.*$" associated with ClassName
    examples/test.cpp:28:9: "b" does not match "^m_.*$" associated with ClassMemberVariable
    examples/test.cpp:31:5: "main(int, const char **)" does not match "^[A-Z].*$" associated with FunctionName
    Total number of errors = 3

### Recursively search all files under 'examples' directory for naming violations, but exclude '*.cpp' and '*.h files
    ./ncc.py --style examples/ncc.style --recurse --exclude *.cpp *.h --path examples

    examples/test.hpp:4:7: "Test" does not match "^C.*$" associated with ClassName
    examples/test.hpp:12:9: "t" does not match "^m_.*$" associated with ClassMemberVariable
    examples/test.hpp:19:9: "_aaa" does not match "^[a-z].*$" associated with StructMemberVariable
    examples/test.c:8:9: "_b" does not match "^[a-z].*$" associated with StructMemberVariable
    examples/test.c:9:9: "_c" does not match "^[a-z].*$" associated with StructMemberVariable
    examples/tmp/test.hpp:4:7: "Test" does not match "^C.*$" associated with ClassName
    examples/tmp/test.hpp:12:9: "t" does not match "^m_.*$" associated with ClassMemberVariable
    examples/tmp/test.hpp:19:9: "_aaa" does not match "^[a-z].*$" associated with StructMemberVariable
    Total number of errors = 8

## License

Copyright © 2018 Nithin Nellikunnu

Distributed under the MIT License (MIT).

## Thank You
Daniel J. Hofmann
