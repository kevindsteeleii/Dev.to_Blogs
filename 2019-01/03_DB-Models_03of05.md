---
title: Database models and ERDs for Newbs Part: 3
published: true
description: A digest-size breakdown of database modeling and entity-relationship models/diagrams.
tags: beginner, databases, SQL
---

## Recap from Last Time

Last time, we looked at a mock school registry with 3 tables: students, professors, and the join table of course registrations. I also promised to do some coding and that's what I intend. So here we go!

Remember This?
![has many through](https://i.ibb.co/N2dmN9n/has-many-through.jpg)

So what's wrong with this?
- course registrations only join students to professors (no courses to be seen)
- we need to record the classes/courses themselves w/ their own id numbers, names, etc 
- you need to be able to generate a student roster for individual classes

## Fixing the Problem

So here's what I came up with.
![updated has many through](https://i.ibb.co/BgLRdfM/many-to-many-2.jpg)

So we revised the models and their relationships in the following ways:
- made it so that a single course **belongs-to** a professor
- course registrations **belongs-to** both courses and students
- a course registrations entity **has** a professor through its course it **belongs-to**

Next, we'll see what a row of the course registrations table looks like now as opposed to before

Before:

|id|professor_id| student_id| 
|-------|-------|------|
|123|37494|746384684|

After:

|id|course_id| student_id| 
|-------|-------|------|
|123|7893726|746384684|


Why all the id numbers?
_High-cardinality_ is the ideal for SQL databases and this solution promotes high-cardinality more than the previous version. It's more reasonable to store references to the model than to clone the database models for a few reasons. Especially since when you have to update or delete a model. If you made clones instead of used references, you would have to repeat the same operations in multiple places and that would lead to mistakes so references are used instead.

Introducing Foreign Keys
The course_id and student_id are the references used in my example and they have a specific name, **foreign keys**. Foreign keys don't need to be named after anything in particular but it should make sense so when I create a row in my course registrations table, I name the column for the course model's id number course_id and follow the same for student_id.

So, that's it for now but tune it next time when I finally throw some code up to show how I would set up these tables.
