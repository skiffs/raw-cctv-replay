# RAW Access SDK #

The following is taken from the README file of the SDK.

This directory contains the RAW Access SDK - a kit to help you develop
access modules for Project RAW, allowing the RAW user interface (and
other programs using the API) to access data held on DVRs from various
vendors.

At present, the SDK only runs well under Linux. It should work on
32 and 64-bit systems, but is not supported on Windows or Mac OS X.

Binaries are provided for Linux/x86, but you are encouraged to build
them yourself from the provided source code - see [Building the SDK](SDK#Building_the_SDK.md) later on in this document.

The RAW Access SDK contains:

  * The API for writing modules (_include/access/module.h_, _include/access/errors.h_)

  * A sample null module (_ac\_modules/libacplugin\_null.so_, _bin/mkzeroimg_)

  * A document (_`docs/ProfilesAndLevels.txt`_) describing which entry points you must support for various profiles of use.

  * A C library for module implementors (_include/access/utils.h_, _include/access/cdc.h_, _lib/acutils.so_) including routines to perform date calculations for you and a unit test set (_bin/test\_utils_)

  * A C++ library for module users (_include/aclib_, _lib/libaclib.so_)

  * An automated test framework for testing modules (_bin/actest_,   _bin/run\_suite.py_, _examples/_, _tests/_)

Source code for all of these components is available in the _src/_ directory.

## Building the SDK ##

You are encouraged to build the SDK yourself. You can do this from the top level::

> _$ make distclean_

To remove the old binaries, followed by::

> _$ make_

If you want the compiled files to go somewhere other than the current directory,you can set DESTDIR::

> _$ export DESTDIR=/some/where/to/put/binaries_

Building the SDK also creates a _$DESTDIR/bin/setvars_ script which you can source to set some environment variables used by the rest of the SDK.

## Environment variables ##


Several environment variables are used by the SD:

  * _RAW\_SRC_
> > The location of the SDK source

  * _RAW\_OBJ_
> > Location the SDK was built in (_DESTDIR_ if you set it, _RAW\_SRC_ if you didn't)

  * _PATH_
> > Should contain _RAW\_OBJ/bin_

  * _LD\_LIBRARY\_PATH_
> > Should contain _RAW\_OBJ/lib_

  * _RAW\_MODULES_
> > Contains the location for the RAW modules you want to load. setvars sets it to _RAW\_OBJ/ac\_modules_

  * _ACTEST\_TEST\_DIR_
> > Contains the location of tests loaded by the test system.  setvars sets it to _RAW\_OBJ/tests_


## Quickly Running Some Tests ##


To run some quick tests against the null module:

  1. Build the SDK
  1. Source _DESTDIR/setvars_::


> _$ . ./bin/setvars_

  1. Run the null module's test suite::

> _$ run\_suite.py suites/null.xml_

You should see output a bit like this::
```
  > actest  --module null  --disc zeroes.indexed /opt/kynesim/projects/062/tree/deploy/sdk/tests/base/load-module.xml /opt/kynesim/projects/062/tree/deploy/sdk/tests/generate/suites/null.xml/base/load-module.generated
  XML input: /opt/kynesim/projects/062/tree/deploy/sdk/tests/base/load-module.xml
  Output file: /opt/kynesim/projects/062/tree/deploy/sdk/tests/generate/suites/null.xml/base/load-module.generated
  Module directory: /opt/kynesim/projects/062/tree/deploy/sdk/ac_modules
  Disc directory: /opt/kynesim/projects/062/tree/deploy/sdk/tests/discs
  Module name: null
  Disc name: zeroes.indexed
  Parsing XML from /opt/kynesim/projects/062/tree/deploy/sdk/tests/base/load-module.xml
  Request: RequestT <- /opt/kynesim/projects/062/tree/deploy/sdk/tests/base/load-module.xml
    Disk = /opt/kynesim/projects/062/tree/deploy/sdk/tests/discs/zeroes.indexed (fd = 4)
   OutFd = 3
   Module = null (in /opt/kynesim/projects/062/tree/deploy/sdk/ac_modules/libacplugin_null.so ) 
   Commands: 
    load-module 
    -------- 

  Running .. 
  Done.
  > cmp /opt/kynesim/projects/062/tree/deploy/sdk/tests/generate/suites/null.xml/base/load-module.generated /opt/kynesim/projects/062/tree/deploy/sdk/tests/expect/suites/null.xml/base/load-module.expected
  /opt/kynesim/projects/062/tree/deploy/sdk/tests/generate/suites/null.xml/base/load-module.generated /opt/kynesim/projects/062/tree/deploy/sdk/tests/expect/suites/null.xml/base/load-module.expected differ: byte 20, line 1
  ! Test base/load-module failed (generated = /opt/kynesim/projects/062/tree/deploy/sdk/tests/generate/suites/null.xml/base/load-module.generated, expected = /opt/kynesim/projects/062/tree/deploy/sdk/tests/expect/suites/null.xml/base/load-module.expected)

...and so on...  ::

  XX tests ran, XX passed, 0 failed.
  `**` OK `**`
```

## How test suites work ##

Tests are described by test suites, conventionally located in $RAW\_OBJ/tests/suites/ .
These are XML files::
```
  `<actest-suite>
    <module>null</module>
    <disc>zeroes.indexed</disc>

    <test>
     <name>base/load-module</name>
     <run>base/load-module.xml</run>
     <expect>base/load-module.expected</expect>
    </test>
     
     ..
  </actest-suite>`
```
  * _`<module>null</module>`_ directs the suite to run against _$RAW\_MODULES/libacplugin\_null.so_.
  * _`<disc>zeroes.indexed</disc>`_ directs the suite to run against _$RAW\_OBJ/tests/discs/zeroes.indexed_.

There then follow a series of tests. The example above implies:

  * _`<name>base/load-module</name>`_  - Gives a name to the test
  * _`<run>base/load-module.xml</run>`_ - Points to _$RAW\_OBJ/tests/base/load-module.xml_ as the test file.
  * _`<expect>base/load-module.expected</expect>`_ - Running _base/load-module.xml_ against the given module and disc should give the output in _$RAW\_OBJ/expect/base/load-module.expected_ in order to pass the test.

...and that's it.

Further documentation can be found in _src/actest/docs_ under this directory.

## How tests work ##

Each individual test is described by a separate XML file, which looks like::
```
  <?xml version="1.0" ?>

  <actest>
   <commands>
    <command type="load-module" />
     ...
   </commands>
  </actest>
```
These commands instruct the test engine to perform various actions. The results are logged in a 'generated' file and then compared against the 'expected' file. If the generated and expected files do not match exactly, a test failure is reported.

Available commands are described in _docs/actest/commands.txt_.

## Writing your own module ##

RAW access modules are plain old shared libraries. Each has a single entry point::

```
int am_module_create(am_module_operations_v1_t **ops, am_host_operations_v1_t *host_ops, const char **abi_version_supported) 
```


In exchange for an _am\_host\_operations\_v1\_t_ structure that provides access to the underlying storage and a way of supporting errors, this entry point supplies:

  * A module operations structure with which to ask the module to perform various operations.
  * The ABI version supported by the module.

At present, if you set abi\_version\_supported to any string other than
AM\_ABI\_VERSION\_ONE, clients will likely refuse to load your module.

The operations you need to provide are documented in _include/access/module.h_ and there is a sample 'null' module in _src/acinterface/null/null\_module.c_

If you want to return errors, there is a list of error codes in _include/access/errors.h_

## Packaging and delivering access modules ##

Access modules should be packaged in a tarfile which expands to
provide either:

  1. For source access modules, a Makefile with a default target which leaves a libacplugin\_XXXX.so file in _lib/_
  1. For binary access modules, one of:

  * i686-pc-linux-gnu/libacplugin\_XXXX.so     (Linux/x86)
  * x86\_64-pc-linux-gnu/libacplugin\_XXXX.so   (Linux/x86\_64)

A registry of access module names is held by Richard Watts
<rrw@kynesim.co.uk>: please register the name of your module to
avoid naming conflicts. The current state of the registry can
be obtained by email from the registrar's address.

A similar registry of architecture names is maintained, again
at the same email address.


## Utilities for module authors ##

The lib/libacutils.so library is provided as a service to those writing
RAW access modules. It incorporates a recent
[cdatecalc](http://code.google.com/p/cdatecalc) library for performing date and
time calculations and provides routines to;

  * Translate strings to and from _am\_string\_v1 format_.
  * Translate access module dates and times to and from cdatecalc dates and times.
  * Provide host operations for UNIX.
  * Translate ac module errors to strings for debugging.
  * Dump hex data.


## Utilities for module users ##

_lib/libaclib.so_ (and associated include files in _include/aclib_) provide a C++ library for module users and test harnesses; please read the header files for details.


## Adding your own commands to actest ##

Module tests are run using a C++ program called actest, one test per process. The source for actest is in _src/actest_ and you can add your own commands following the code in _src/actest/basecommands.cpp_ .