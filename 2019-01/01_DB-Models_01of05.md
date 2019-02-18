---
title: Database models and ERDs for Newbs Part: 1
published: true
description: A digest-size breakdown of database modeling and entity-relationship models/diagrams.
tags: beginner, databases, SQL
---
## So why another database post?

Hi everybody, I would like to introduce something very basic to newbies or folks starting out with the backend of development. This post will be replete with diagrams because we all have different learning styles and visual aids are always a great way of breaking up the text. As an aside, I am not a database expert or DBA, I welcome and appreciate any feedback, comments, or corrections from all the code senpai out there.

So let’s get started with some working definitions.
The wiki definition of a database model is pretty good, so we’ll start there: 

>“A **database model** is a type of data model that determines the logical structure of a database and fundamentally determines in which manner data can be stored, organized and manipulated. The most popular example of a database model is the relational model, which uses a table-based format.”

A data model is used to represent or imitate an entity. An entity is basically a noun. Some are abstract like math, and others are concrete (has a physical form) like a shoe. Let's take a look at a table of students.

![Diagram of a student body](https://thepracticaldev.s3.amazonaws.com/i/xe1v1ud681pcfqcqfqgx.jpg)

This database model takes the form of a table, the rows represent distinct students while the columns represent an attribute or quality the student has. Each column is of a specific data type and that helps makes the standardized manipulating and reading of student data possible. If all entries of the columns were of a different type, writing queries would be a pain. I’m now going to introduce a couple more important terms, **normalization**, and **cardinality**. **Normalization** is the process used to reduce the redundancy of data by sometimes splitting a database into two or more tables. **Cardinality** would be considered high if there were very few duplicate bits of data in the same column, low cardinality tables have a lot of duplicates.
An **Entity-Relationship Diagram** or model is used to map the potential relationships between data models. By potential, I mean that some of these relationships are strictly optional. For example, a college professor could teach classes it does not mean they do. However, to have a class you need a professor and at least a student.

So what does this actually mean to us [developers]?

We use database models and ERDs as developers to map out the models and their relationships so that we can manipulate and read what’s stored on the database. Their design determines the level of functionality so please keep that in mind. The function determines the form in this case.

Stay tuned for next time where we will explore how to draw these diagrams using crow's notation.

