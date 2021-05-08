Gremlins is a python program/framework which assists in fault testing distributed systems.

Overview
=========

Gremlins is a fault injector - it is an evil program that sits on a machine and does
nasty things to other programs on that machine (or the machine overall).

Its primary purpose is for black-box long-lived testing of a distributed system, as it
does not make any effort to provide concepts like "test cases" or code instrumentation.
The idea is not to trigger specific error cases, but to simulate generally faulty hardware
and networking so that a larger class of problems can be found on a small test cluster.

The hope is that, if a fault tolerant system can make progress without corruption or
unrecoverable errors on a 5-node cluster full of gremlins, it will also be free of such
errors on a 500-node cluster where errors may occur every day by natural causes.

Setup
=====

The very simplest way to run gremlins is to just set your python path:

$ PYTHONPATH=. ./gremlins/gremlin.py

The second simplest way (and the recommended one) is to run it within a python virtual environment
after running python setup.py develop

$ gremlins

Concepts
========

Gremlins is built around a few key concepts: faults, triggers, and profiles.

Faults
------

A fault is the most specific unit of abstraction - it is simply a thing that can go wrong.
One example fault is "kill -9 the DataNode JVM, wait 60 seconds, then start it back up".
Another example might be "turn off networking for 5 minutes"

Faults are simply python callables. Anything that can be called can be run by the framework.

Some handy faults are provided in the gremlins.faults module. Note that most of these faults
are functions that return other functions. This is a useful pattern, though some people
might prefer making classes whose instances are callable.

A related concept is "metafaults". These are simply faults that provide nice containers around
other faults. Currently the only example of a metafault is gremlins.metafaults.pick_fault,
which takes a list of (weight, fault) pairs, and picks one of the subfaults according to the
provided weights.

Triggers
--------

A trigger is a way of running faults. The simplest trigger (and the only one that really works
well at the moment) is gremlins.triggers.Periodic. This trigger is constructed with an interval
and a fault. It simply repeats a process of sleeping for the given interval, and then running
the fault.

Another trigger in development is the webserver trigger. This exposes a CherryPy webserver
which accepts POST requests (eg via curl) so that cross-machine fault testing can be controlled
from a central location.

Future trigger ideas include the ability to watch a log for a given line before triggering a fault,
etc.

Profiles
--------

A profile currently doesn't have a type, but is just a normal python list of triggers. When
running gremlins, one can provide a profile, and each of the triggers will be started.
This concept allows one to start both a webserver trigger and a periodic trigger from a
single invocation.

Running gremlins
================

Gremlins can be run in two different modes. In the first mode, the user specifies a list of faults.
These faults are executed immediately, and then gremlins exists. In the second mode, the user
specifies a Profile to start. This profile is run until the user kills the gremlin process.

For example, to run the hbase.rs_pause fault just once, simply execute:

  $ gremlins -m gremlins.profiles.hbase -f hbase.rs_pause

The -m flag causes gremlins to import the given python module. This can be useful to specify
faults from a module that is not included with gremlins itself.

Multiple faults can be executed in sequence by passing multiple -f options.


To run a fault profile, simply pass it with a -p flag:

  $ gremlins -m gremlins.profiles.hbase -p hbase.profile


