# Sky -- Open Source Behavioral Database Management System (BDBMS)

## Overview

Sky is a system for analyzing behavior for a given object and aggregating and
segmenting that behavioral analysis across all objects in the system.

The basic unit in Sky is the Event. An Event consists of two types of data: an
action & a state change. Both are optional but an event needs at least one to
exist. An action defines something that has occurred such as a `purchase` or a
`sign up`. A state change defines a change in one or more properties on the
object such as `name` or `favorite color`. An Event also includes a millisecond
resolution timestamp that shows when it occurred.

Events for an object are grouped together into a Path. An object only has one
path although a path can be sliced into one or more subpaths. An example of a
subpath would be a session on a web site where a user might view several web
pages at a time with a certain minimum idle time between visits.

An Object has a 64-bit positive integer identifier that can be correlated to
a source system's primary key. By traversing the events within an object's path,
the object's state can be rebuilt for any given point in time. This also means
that actions can be queried based on the state of an object at the time they
occurred.


## Goals

More than anything the Sky server is built around *simplicity*. This is
reflected in the code that is written as well as the features that are added.
Complexity can be offloaded to an external language on a per case basis.


## Roadmap

Sky is a young project but this road map is meant to provide an overview of
where it is headed. The following is what is coming up:

1. Standalone Server - A simple server to store and retrieve events and
   paths for an object.
1. PQL Query Engine - Parsing, lexing and execution of a PQL query.
1. Write Ahead Log - Periodically write events to the database to improve write
   performance.
1. Cache - Cache paths in memory for active objects.
1. Real-Time Queries - Adjust query results in real time as events come in.
1. Plug-ins - Allow external code to be used to process event data for things
   such as machine learning.
1. Distribution - Distribute paths across multiple machines with built-in
   sharding and failover.


## Path Query Language (PQL)

The SQL language was built to query or alter the current state of an object in a
relational database. Sky, on the other hand, is meant to query the state and
actions of objects across time. Because of this a new query language is needed.

The Path Query Language (PQL) is designed with these specific aims:

1. Encapsulated - Only a single path is queried at a time.
1. High-Level - The language only works with high level objects - events & paths.
1. Aggregation Only - The language on queries the database. It does not change
   or add data to the database.


## Contribute

If you'd like to contribute to Sky, please fork the repo on GitHub:

https://github.com/skylandlabs/sky

You're also welcome to discuss the project on the mailing list by sending an
e-mail to [sky@librelist.com](mailto:sky@librelist.com).
