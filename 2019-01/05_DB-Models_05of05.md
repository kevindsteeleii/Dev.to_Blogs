---
title: Database models and ERDs for Newbs Part: 5
published: true
description: A digest-size breakdown of database modeling and entity-relationship models/diagrams.
tags: beginner, databases, SQL, postgres
---
# The CRUD operations
## Recap
Last time we delved a bit into SQL using PostgreSQL's command line tool, psql. The database was created, tables made, and rows inserted.

## What now?
This is a bit unorthodox but I'm trying to ramp up to 2 posts a week on average so I'm concluding this series here. But, before I close on this, I'll be going over a few things in SQL. Specifically how we insert rows into our join tables, make instances/rows of the models the join table refers to, update a row, and finally delete a row and delete the whole dang database. So I'll write up some scenarios with them to justify doing the code.

Let's access our database. 

![access database](https://i.ibb.co/N3GCTYq/2019-02-05-001.png)

Since we already have made the database in the last entry this is how we access it using psql.

### Creating rows!
**Scenario**: Professors Elizabeth King and James Marshal just got hired to teach a couple of classes. They need to be entered into the database before their courses can be determined.

![insert new professors](https://i.ibb.co/bK71Vdz/2019-02-05-002.png)

**Professors Table**:

|id | first_name| last_name|
|----|----------|----------|
|1| James| Marshal|
|2| Elizabeth| King|


**Scenario**: The newly hired Professors Marshal and King teach an English and Math course respectively.

![insert courses](https://i.ibb.co/TRnVs9N/2019-02-05-003.png)

**Courses**:

|id|title|description|professor_id|
|---|---|---|---|
|1|Freshman Math|A mathematical survey of the...|2|
|2|Middle English|Middle English, Chaucer and beyond|1|

**Scenario**: Student ID number 1, Adam Bean registers for both of the new courses taught by the new professors. Student ID number 2, Clara Doe registers for only the Math class since she transferred with the appropriate pre-reqs. And Student ID number 3, Everett Franklin just wants to read Chaucer so he registers for Marshal's course.

![insert course registrations](https://i.ibb.co/YhVQwgp/2019-02-05-004.png)

Here, we have inserted professors, courses, and the course_registrations. Pay close attention to the course_registrations table. It only has its own id number and two foreign keys, one refers to a course row and the other to a student.

**Course_Registrations**:

|id|course_id|student_id|
|---|---|---|
|1|2|1|
|2|2|3|
|3|1|1|
|4|1|2|

### Reading from a single student with ID of 2. 
**Scenario**: Clara needs to be looked up to confirm some information for the admins.

![select student 2](https://i.ibb.co/BVNyjqm/2019-02-05-005.png)

### Updating a student's last name.

**Scenario**: Clara gets married and wants to adjust her student info to reflect her legal status. This is how you would change her name.

![update student 2 last name](https://i.ibb.co/Dw1tRVM/2019-02-05-006.png)

### Deleting a row.
**Scenario**: Everett wants to transfer to a school that better fits his needs and so his record needs to be removed. We delete a row like this:

![delete student 3](https://i.ibb.co/PGr0xhK/2019-02-05-007.png)


### Droping the database.
**Scenario**: The college is about to close down but their database contains sensitive information so the entire database needs to be deleted. The following code is how you would remove or _drop_ the database.

![drop database](https://i.ibb.co/2M54DdV/2019-02-05-008.png)

And there you have it CRUD! I had a lot of fun making the diagrams on such over the last 5 posts or so and would be open to any feedback. Thanks for reading!