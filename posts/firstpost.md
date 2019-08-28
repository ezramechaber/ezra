---
title: Finally learning SQL a decade into my career
description: It's what it sounds like.
date: 2019-08-27
tags:
  - learning
layout: layouts/post.njk
---

I know HTML, I know CSS, I can write a little bit of Javascript when my life depends on it. But put me in front of a database and ask me to pull records using SQL and my whole body freezes up. I've been around it my entire career—paralyzed by `INNER JOIN` and `SELECT *` —but I've never learned how to use it/write it/.

#### A History of Muddling Along
I remember seeing my first query. I was in the basement of the EEOB during the Obama White House trying to figure out how to do A/B/N tests in ExactTarget. A coworker, our lead/only data scientist with multiple advanced degrees who was in the middle of trying to help save HealthCare.gov helped pull together the code—a task I now understand to be somewhere between years and decades below his level of seniority. 

He was fiercely patient, explaining each query to me, and helping me craft small adjustments. But I could never get the hang of it enough to pull the kind of data I wanted.

That was 2013. I still don't know how to do my own SQL work, settling for bad GUIs wherever possible. That let me get through two more jobs and six years. An attempt at a Codecademy course, an O'Reilly book found on a Brooklyn stoop, and several more critical databases didn't improve the outcomes.

#### Setting Up a Perfect Storm
But now at Glitch, a perfect storm conspired to make me SQL-literate. But it wasn't—and someone told me this once—until I really needed it to do something I couldn't achieve any other way that I learned how to use SQL.

The reasons that ultimately led to that "something I couldn't achieve any other way" were as follows, in order of importance:
* Gina Tripani's  dotfiles config included the homebrew  install for SQLite.
* Glitch is built on a culture of learning and shared expertise (which I will get to shortly).
* Users with multiple user account id's linked to identical email addresses weren't being house-holded correctly. Almost nothing makes a former emailer less happy than phantom duplicates.
* I don't have Excel installed and Numbers maxes out after a certain number of rows.

For the last several months, I've been partnering with different engineers on pulling ad hoc queries from our database tool for metrics. Our tool is built with MySQL support, and some of the more complex questions I've been asking require using the query builder.

Watching complex SQL written in front of you when you don't know the proper syntax or structure is like watching someone take notes using a personal steno shorthand. It's a disaster.
* Most databases have their own names.
* Everyone I've ever met has their own preferred aliases/nicknames when handling tables and columns.
* Everyone has a different thought process—some people get right to writing in SQL, and some people write out pseudo code. If you don't know what's what, following the build process doesn't make any sense.

Yeah. So watching someone sketch out `SELECT table.email AS t.e` , it was like… what am I even looking at here?

But I did start to pick a few things up. First you need a database and a table or two. Then you need to populate those tables with some data. To manipulate it, you start with a SELECT query. Add some conditions (thank you Google + SQLite documentation), a GROUP BY, and you start to figure out how to show some basic stuff: give me a count of every row, then give me a count of every row with a sign-up date before X (do some extra googling if it's unicode-formatted), etc.

So there I was, sitting on my computer with a .csv of email addresses and trying to solve a very particular question: *How do I get a count of email addresses (who were not signed up for our platform) and figure out how many of them converted after an email about the platform?*

#### Enter SQLite
Apple's Numbers.app has a limit of 65,000 rows or so. Google Sheets is good for many things, but specific de-dupes and comparisons (unless you're up for Macro work) is not one of those things. 

Enter: SQLite. I remembered that as part of setting up my own dotfiles (using Holman/Gina Tripani's examples), I had left SQLite as a Homebrew install. Why not give it a shot?

[image:BEB33040-E7CF-4D9A-8BFE-A34C536A27DE-668-00001BB0B1CB8585/Screen Shot 2019-08-25 at 2.37.21 PM.jpg]

#### Enter Google (Muddling Around 2: The Re-Muddling)
I love a GUI. SQLite is not that. So… I needed some help if I was going to manipulate data I couldn't even see.

Some documentation and help files are not as useful as others, though. This… is not a page meant to help people new to database design:

[image:638F6D47-1E79-466E-9C0B-56606AADA5CB-668-00001BD83196B056/Screen Shot 2019-08-25 at 2.40.41 PM.jpg](https://www.sqlite.org/lang_createtable.html)

This is more like it:

[image:61CC94C6-FF18-42A8-B4F0-30259A2842D1-668-00001BECB3FA53D6/Screen Shot 2019-08-25 at 2.42.42 PM.jpg](http://www.sqlitetutorial.net/sqlite-import-csv/)

And, of course, how anyone survives in the world without Stack Overflow is a mystery to me. The first problem I ran into is that Customer.io (our email service) was spitting out timestamps in Unix format. MySQL [makes that easy](https://database.guide/unix_timestamp-examples-mysql/). SQLite is a little bit different. The [Stack Overflow answer](https://stackoverflow.com/questions/14629347/how-to-convert-unix-epoch-time-in-sqlite) I found for worked like a charm:

```
UPDATE all_signups SET created_at = datetime(created_at, 'unixepoch', 'localtime');
```

#### Documenting What I Learned
Most of the time when I'm working in Terminal, I'm copying/pasting and just trying to get through my task. Today I was trying to learn something.

So as I went about it, I started treating this like a homework assignment, figuring out what each step of the query might be. I wrote each line in VS Code and saved it in a .sql file alongside an explanation of what worked and why it worked:


[image:AD50B07E-6DE7-4D50-81E5-98EC417A807A-668-00001C4E33C83DFA/Screen Shot 2019-08-25 at 2.49.14 PM.jpg]

#### What Was the Answer?
The answer to this question—how many people converted—was crazy low. That was a bummer.

But as the old adage goes, the real conversion was the SQL we learned along the way. Or something like that.

The process of researching, documenting, and ultimately understanding the syntax/behavior of SQL was so valuable that the disappointing answer of conversions came out in the wash. I'm newly self-sufficient in a few valuable new ways. While I will surely forget plenty of what I learned between now and my next query, I feel like I truly grasped the premise for the first time, making my next time -muddling- googling around a way less painful endeavor. By writing all of this down, I'm hoping to commit even more to memory. And because I've simultaneously been on a project to write more things down, maybe it'll improve my writing, too.

