Unified Test Automation Platform [UTAP]
===============

.. contents::
   :local:

Introduction
------------

**Unified Test Automation Platform [UTAP]** is aimed at solving the test automation needs of XYZ with primary focus to APIs, Web and Mobile test automation. 

This platform will consist of **Test Automation Framework [TAF]** that is built using Robot Framework and External Libraries available in the ecosystem. 

In addition, the platform also enables CT (Continous Testing) by providing a test environment that is Dockerized. This test environment will also establish necessary connections towards System/Application Under Test (SUT/AUT). Needless to say, the environment is integrated with ALM Octane to feed the automated test results.

`Robot Framework <http://robotframework.org>`_ is a generic open source
automation framework for acceptance testing, acceptance test driven
development (ATDD), and robotic process automation (RPA). It has simple plain
text syntax and it can be extended easily with libraries implemented using
Python or Java.

Robot Framework is operating system and application independent. The core
framework is implemented using `Python <http://python.org>`_, supports both
Python 2 and Python 3, and runs also on `Jython <http://jython.org>`_ (JVM),
`IronPython <http://ironpython.net>`_ (.NET) and `PyPy <http://pypy.org>`_.
The framework has a rich ecosystem around it consisting of various generic
libraries and tools that are developed as separate projects. For more
information about Robot Framework and the ecosystem, see
http://robotframework.org.



Installation
------------

Prerequisites:

- `Python Installation
  <https://www.python.org/downloads/>`_
  
- `Eclipse Instllation
  <https://wiki.eclipse.org/Eclipse/Installation>`_

- `Eclipse RED Plugin Installation
  <https://marketplace.eclipse.org/content/red-robot-editor>`_

TAF can be installed by cloning the project from this repository.

Web Test Automation Example
-------

Below is a simple example test case for testing login to some system. More examples are available in examples folder in this project.

.. code:: robotframework

    *** Test Cases ***
    Valid Login
        Open Browser To Login Page
        Input Username    demo
        Input Password    mode
        Submit Credentials
        Welcome Page Should Be Open
        [Teardown]    Close Browser

API Test Automation Example
-------

Below is a simple example test case for testing REST api service. More examples are available in examples folder in this project.

.. code:: robotframework

    *** Test Cases ***
    Valid Return Code
        GET Request    url    resourcePath    headers
        Verify Response Code    200

Usage
-----

Tests can be executed from the command line using the ``robot`` script or by executing the ``robot`` module directly like ``python -m robot`` or ``jython -m robot``.

The basic usage is giving a path to a test (or task) file or directory as anargument with possible command line options before the path::

    robot tests.robot
    robot --variable HOST:example.com --outputdir results path/to/tests/

Additionally there is ``rebot`` tool for combining results and otherwise
post-processing outputs::

    rebot --name Example output1.xml output2.xml

Run ``robot --help`` and ``rebot --help`` for more information about the command
line usage. 

Documentation
-------------

- `Test Automation Framework User Guide
  <http://robotframework.org/robotframework/#user-guide>`_
- `Drivers with Keywords
  <http://robotframework.org/robotframework/#standard-libraries>`_
- `General documentation and demos
  <http://robotframework.org/#documentation>`_

Support and contact
-------------------

- `utap-users
  <https://groups.google.com/group/robotframework-users/>`_ mailing list
- `Slack #test-automation <https://robotframework-slack-invite.herokuapp.com>`_ channel
