---
layout: post
title: My experience with learning SQL
thumbnail: /media/images/SQL.png
---

![SQL]({{ baseurl }}/media/images/SQL.png)

Today, I finished the third class of SQL (about its syntax and [Microsoft SQL Server](en.wikipedia.org/wiki/Microsoft_SQL_Server
)) in my university, where we have been taught about [SQL Joins](http://www.techonthenet.com/sql/joins.php) (Inner Joins, Outer Joines, etc.) and [Subqueries](https://technet.microsoft.com/en-us/library/ms189575%28v=sql.105%29.aspx).

Even though, it was my first time learning the actual SQL Queries (the first two classes were introductory classes and thus were boring for me), it convinced me enough that SQL isn't hard to learn for newbies compared to general purpose programming languages like C/C++, Java, etc.

My conviction was further increased when I read about it on the internet. I came to this conclusion for the following reasons:

### 1) Separation of church and state

[RDBMS](http://en.wikipedia.org/wiki/Relational_database_management_system) is separated from SQL; you do not need to learn about the inner details of RDBMS in order to learn SQL. Most SQL code is portable across different RDBMS.

### 2) Writing SQL queries is similar to writing pseudocode

SQL is very [declarative](http://en.wikipedia.org/wiki/Declarative_programming) unlike most procedural programming languages (C/C++, Java, etc.). You can just throw a bunch of keywords and expect good things to happen! Consider the following SQL query:
{% highlight SQL %}
SELECT * FROM Customers
WHERE Country='America';
{% endhighlight %}

It's pretty obvious from the code that we are asking for a table with name of Customers who lives in America.

### 3) Tables are ubiquitous

You can play with predefined tables; you do not need to learn about tables / schemas and their different formats. Most RDBMS also supports reading / writing Microsoft Excel files.

## Conclusion

Overall, I find SQL very easy to learn because of its eloquent syntax, although I felt a bit lack of intuition in its syntax considering it was initially developed in the 70s. I will be updating on my journey to learn SQL, so stay tuned!
