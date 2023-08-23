---
title: "Final Report"
date: 2023-08-23T14:38:50+05:30
draft: false
---

## Introduction

My Google Summer of Code project was done under the `Ste||ar Group` organisation.
The project was to bring the `HPXIO` library up to date with HPX and to build upon it. `HPXIO` is a library written using
`HPX` for asynchronous and fast I/O. The goal is to provide an interface for several I/O operations in distributed and parallel systems.

## Work Done

All of the work done is contained in the following pull request : [click](https://github.com/STEllAR-GROUP/hpxio/pull/7) 

The work consisted mainly of the following tasks:

- Updating the `HPXIO` library to work with the latest version of `HPX`.
  
Initially the libraryhad a very basic module using I/O thread pools. This was written for an older version of HPX and did not compile.
I fixed the compilation errors and updated the code to work with the latest version of HPX.

- Adding a new class `hpx::io::io_dispatcher`

This class was added to provide an interface to distribute I/O requests between several compute nodes or threads. This uses several
instances of the clas `hpx::io::local_file` which can use I/O threads to perform I/O operations.
Both the classes uses components and actions to perform the I/O operations. The design is based upon the `ShenEOS` example in HPX.

- Adding algorithms for I/O

Some algorithms were discussed and added to the `hpx::io::local_file` class. These include lazy writing and read caching. The aim is to hide
as much latency as possible.

- Write a test file

The test file `io_dispatcher_test.cpp` was written to test the functionality of the library. It is configured using command line options and uses a Timer class to measure the time taken for the I/O operations.

## Challenges Faced

The main challenge was to figure out the existing codebase to build upon it. The library uses a lot of HPX facilities such as `components, actions, futures, serialization` etc. I had to learn about these concepts and incorporate them in my code.

Another challenge was to write bug free code. The bugs in an HPX program are hard to debug because of the multi-threaded nature. Nevertheless I got used to debugging the applicaiton.

## Future Work

Future additions to the library may include:

- Adding more tests and benchmarking
- Adding a Senders/Receivers interface to the library using HPX facilities