---
title: Database models and ERDs for Newbs Part: 4
published: true
description: A digest-size breakdown of database modeling and entity-relationship models/diagrams.
tags: beginner, databases, SQL, postgres
---

## Recap
So last time we fixed up the students, professors, and courses relationship. This was done by the amazing application of *join tables*. Join tables basically, hold references for 2 or more database models that would otherwise have a _many-to-many_ relationship. Which is problematic because it creates a situation where data is duplicated in a bunch of places, leading to low _cardinality_. Cardinality basically refers to how unique data is in a particular column. While join tables aren't perfect, it's better than keeping entire copies of rows (individual instances of the model) nested in other rows.

## Corrections
I made an assumption about the data model for the student based on the desire to show a greater variety of _crow's foot notation_. But the _has one or more_ course_registrations demarkation of the student is confusing when you think about it. It would lower cardinality so I'm just going to add a boolean data type column called _has_registered_ to alleviate this.

**It took this.**

![has many through](https://i.ibb.co/N2dmN9n/has-many-through.jpg)

**And made it look like this**
![updated has many through](https://i.ibb.co/BgLRdfM/many-to-many-2.jpg)

## Code, yes?

Not quite yet, first some errata. 
1. I am by no means a DBA(database admin) or anything so I'm not going to get too deep into joins in this one.
1. I'm using **PostgreSQL**. If you don't have it, here's a [download link](https://www.postgresql.org/download/).
1. I use an ORM (Object Relational Mapper) in production but you should always know what's going on "under the hood" of whatever abstraction you're using, to a degree. This hopefully sheds some light on what the tools you are using to spin up databases are actually doing.
1. There are visualization tools and managers to help you with your databases like [pgAdmin](https://www.pgadmin.org/download/). Download it, play with it!
1. Forget the UUID thing. It's neat but I don't think introducing modules in PostgreSQL befits a beginner
1. I am also omitting what a full-blown version will look like. There's a lot of data to consider and will go into detail on something similar later.
1. And finally, at this point, I'm assuming you downloaded PostgreSQL and have it set up.

So here we go:

First, we go the terminal, git bash or power shell (you should be using one of these!) and enter the following:
```
psql CREATE DATABASE school_server
```

So in the above code, I entered the DBMS (database management system) and then I created the database that holds my tables. I affectionately called it _school_server_. 

Next up, the tables themselves.

![code to make all of the aforementioned tables](https://i.ibb.co/ckqPVHf/2019-02-03-002.png) 
So here I made the professors, students, courses, and course registrations tables. Pay close attention to _courses_ and _course_registrations_ tables. They both contain some **foreign keys**. 

**Sounds familiar?**
It should, I mentioned previously that foreign keys are used as references that point to the appropriate row in the table that has a relationship with the row that contains that foreign key. 

In the case of the courses and course_registration tables, we see 3 different foreign keys. Courses have only one, in the _professor_id_ column. Course_Registrations has two because it is a **join table** that joins together courses and students. Which are also what its foreign keys point towards. So let's have a gander at what these newly-minted tables look like.


**Professors**

|id | first_name| last_name|
|----|----------|----------|


**Courses**

|id | title| description|professor_id|
|----|----------|----------|----------|

**Course_Registrations**

|id | course_id | student_id |
|----|----------|----------|

**Students**

|id | first_name | last_name |has_registered |
|----|----------|----------|---------|

This is getting to be a bit long (vertically). So I'm going to call it quits here but, before I close I'll do show you one more thing.

Create Students!
![creating new students in SQL code](https://i.ibb.co/6gpMmzr/2019-02-03-003.png)

And now our table of students looks like this:

|id | first_name | last_name |has_registered |
|----|----------|----------|---------|
|1 | Adam | Bean |true |
|2 | Clara | Does |true |
|3 | Everett | Franklin |true |
|----|----------|----------|---------|

Next time, I'll cover the getting a specific student's data, updating, and deleting in SQL. See ya!
