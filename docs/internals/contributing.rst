Contributing to Batavia
=======================

If you experience problems with Batavia, `log them on GitHub`_. If you want to contribute code, please `fork the code`_ and `submit a pull request`_.

.. _log them on Github: https://github.com/pybee/batavia/issues
.. _fork the code: https://github.com/pybee/batavia
.. _submit a pull request: https://github.com/pybee/batavia/pulls


Setting up your development environment
---------------------------------------

The process of setting up a development environment is very similar to
the :doc:`/intro/getting-started` process. The biggest difference is that
instead of using the official PyBee repository, you'll be using your own
Github fork.

As with the getting started guide, these instructions will assume that you
have Python 3, and have virtualenv available for use.

Start by forking Batavia into your own Github repository; then
check out your fork to your own computer into a development directory:

.. code-block:: bash

    $ mkdir batavia-dev
    $ cd batavia-dev
    $ git clone git@github.com:<your github username>/batavia.git

Then create a virtual environment and install Batavia into it:

.. code-block:: bash

    $ virtualenv -p $(which python3) env
    $ . env/bin/activate
    $ pip install -e .

Lastly, you'll need to obtain and install `PhantomJS`_. PhantomJS is a
headless browser that allows Batavia to test it's behavior in a "real"
browser. Installation instructions

OS/X
~~~~

PhantomJS can be installed using `Homebrew`_. If you don't already have brew
installed, follow the brew installation instructions, then run::

    $ brew install phantomjs

Alternatively, you can download the PhantomJS tarball, and put the
``phantomjs`` executable somewhere in your path.

.. _Homebrew: http://brew.sh

Ubuntu
~~~~~~

Installation on Ubuntu 14.04 is relatively simple::

    $ sudo apt-get install phantomjs

Raspbian/Raspberry Pi
~~~~~~~~~~~~~~~~~~~~~

This is apparently possible...

.. _PhantomJS: http://phantomjs.org

Running the test suite
----------------------

You're now ready to run the test suite! Type:

.. code-block:: bash

    $ cd batavia
    $ python setup.py test

This will take about 5 minutes on most modern PCs/laptops, and will generate around 4000 lines of console output - one line for each test that is executed. Each line will tell you the pass/fail status of each test - e.g.,::

    test_abs_not_implemented (tests.builtins.test_abs.AbsTests) ... expected failure
    test_bool (tests.builtins.test_abs.BuiltinAbsFunctionTests) ... ok

This indicates that tests have passed (``ok``), or have failed in an expected
way (``expected failure``). These outcomes are what you expect to see. If you
see any lines that end ``FAIL``, ``ERROR``, or ``unexpected success``, then
you've found a problem. If this happens, at the end of the test run, you’ll
also see a summary of the cause of those problems.

However, this *shouldn't* happen - Batavia runs `continuous integration`_ to
make sure the test suite is always in a passing state. If you *do* get any
failures, errors, or unexpected successes, please get in touch, because you
may have found a problem.

.. _continuous integration: https://travis-ci.org/pybee/batavia

If you just want to run a single test, or a single group of tests, you can provide command-line arguments.

To run a single test, provide the full dotted-path to the test:

.. code-block:: bash

    $ python setup.py test -s tests.datatypes.test_str.BinaryStrOperationTests.test_add_bool

To run a full test case, do the same, but stop at the test case name:

.. code-block:: bash

    $ python setup.py test -s tests.datatypes.test_str.BinaryStrOperationTests

Or, to run all the Str datatype tests:

.. code-block:: bash

    $ python setup.py test -s tests.datatypes.test_str

Or, to run all the datatypes tests:

.. code-block:: bash

    $ python setup.py test -s tests.datatypes
