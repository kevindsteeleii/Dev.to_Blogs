---
title: Database models and ERDs for Newbs Part: 2
published: true
description: A digest-size breakdown of database modeling and entity-relationship models/diagrams.
tags: beginner, databases, SQL
---

## Recap from Last Time

So far we covered database models as a way to create abstractions that represent entities, or things with quantifiable attributes. Next, I'll explain some points on relationships and how we go about figuring them out.

## What's Crow's Foot Notation?

Crow's Foot Notation can be traced back to the mid-1970s and something called structured systems analysis and design method if you want to do a little more reading after this. Essentially it's a way of diagramming entities as boxes and their relationships as lines with markings that roughly resemble a crow's foot. It also goes by the name of Barker's notation. With that bit of historical errata out of the way, let's get to the main point.

Why use it?

While we as developers are more than capable of creating amazing databases programmatically, writing code first leads to a lot of mistakes. Mistakes lead to greater cost and cost leads to things that can result in the failure of a venture or product. So just like carpenters, we need to measure twice and cut once. And by the way, you **don't** have to use this specific notation. Use any system that works to design your models and their relationships before you start programming. I'm personally interested in systems design and such, which is why I'm writing this.

What does it look like?

![Crow's Foot Notation Chart](https://i.ibb.co/qjw6dMn/Crow-Notation-Chart.png)

In action?

![Crow's Foot Notation in Action](https://i.ibb.co/XsFLvn2/Crow-Example.png)

Let's unpack this.
The professors can have students but don't necessarily need to have students. Students need to have at least one professor. So imagine a small school that only documents their registered students. The professors may or may not teach a course but all students need to take at least one course to be counted at all for any kind of course credit. However, many-to-many relationships when implemented this way cause low cardinality, or having a lot of duplicated information. See the next figure.

![Many to messy](https://i.ibb.co/mGzVt3m/Many-To-Messy.png)

Join tables to the rescue!

A join table is what it sounds like. It joins related tables and creates rows of matching entities. But, it would only contain references to them not copies to avoid low cardinality. In our case, we use course registrations to join our many students and professors.

![has many through](https://i.ibb.co/N2dmN9n/has-many-through.jpg)

Mind you we could still refine this to make an even better entity relationship diagram but that will have to wait for next week. 

In part 3, we're gonna break this down even more to build a better system. If I'm able to, I'll be adding some code this time around.




