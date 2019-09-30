
# Filtering and Ordering - Lab


## Introduction
In this lab, you will write more `SELECT` statements to solidify your ability to query a SQL database. You will also write more specific queries using the tools you learned in the previous lesson.

## Objectives
You will be able to:
* Limit the number of records returned by a query using `LIMIT`
* Filter results using `BETWEEN` and `IS NULL`
* Order the results of your queries by using `ORDER BY` (`ASC` & `DESC`)

### Famous Dogs

Here's a database full of famous dogs!  The `dogs` table is populated with the following data:

|name      |age    |gender |breed           |temperament|hungry |
|----------|-------|-------|----------------|-----------|-------|
|Snoopy    |3      |M      |beagle          |friendly   |1      |
|McGruff   |10     |M      |bloodhound      |aware      |0      |
|Scooby    |6      |M      |great dane      |hungry     |1      |
|Little Ann|5      |F      |coonhound       |loyal      |0      |
|Pickles   |13     |F      |black lab       |mischievous|1      |
|Clifford  |4      |M      |big red         |smiley     |1      |
|Lassie    |7      |F      |collie          |loving     |1      |
|Snowy     |8      |F      |fox terrier     |adventurous|0      |
|NULL      |4      |M      |golden retriever|playful    |1      |

## Connecting to the Database

First, import sqlite3 and establish a connection to the database **dogs.db**. Then, create a cursor object so that you can pass SQL queries to the database.


```python
#Your code here; import sqlite, create a connection and then a cursor object.
import sqlite3 
conn = sqlite3.connect('dogs.db')
cur = conn.cursor()
```

 

## Queries

Display the outputs for each of the following query descriptions.

### Select the name and breed for all female dogs


```python
#Your code here
cur.execute('''select name breed from dogs where gender = 'F' ''').fetchall()
```




    [('Little Ann',), ('Pickles',), ('Lassie',), ('Snowy',)]



### Select the names of all dogs listed in alphabetical order.  Notice that SQL lists the nameless dog first.


```python
#Your code here
cur.execute('''select name breed from dogs order by name ''').fetchall()
```




    [(None,),
     ('Clifford',),
     ('Lassie',),
     ('Little Ann',),
     ('McGruff',),
     ('Pickles',),
     ('Scooby',),
     ('Snoopy',),
     ('Snowy',)]



### Select any dog that doesn't have a name


```python
#Your code here
cur.execute('''select * from dogs where name is null ''').fetchall()
```




    [(9, None, 4, 'M', 'golden retriever', 'playful', 1)]



### Select the name and breed of only the hungry dogs and list them from youngest to oldest


```python
#Your code here
cur.execute('''select breed, name from dogs where hungry = 1 ''').fetchall()
```




    [('beagle', 'Snoopy'),
     ('great dane', 'Scooby'),
     ('black lab', 'Pickles'),
     ('big red', 'Clifford'),
     ('collie', 'Lassie'),
     ('golden retriever', None)]



### Select the oldest dog's name, age, and temperament


```python
#Your code here
cur.execute('''select name, age, temperament from dogs order by age desc limit 1''').fetchall()
```




    [('Pickles', 13, 'mischievous')]



### Select the three youngest dogs


```python
#Your code here
cur.execute('''select name, age, temperament from dogs order by age limit 3''').fetchall()
```




    [('Snoopy', 3, 'friendly'), ('Clifford', 4, 'smiley'), (None, 4, 'playful')]



### Select the name and breed of the dogs who are between five and ten years old, ordered from oldest to youngest


```python
#Your code here
cur.execute('''select name, breed from dogs where age >= 5 and age <= 10''').fetchall()
```




    [('McGruff', 'bloodhound'),
     ('Scooby', 'great dane'),
     ('Little Ann', 'coonhound'),
     ('Lassie', 'collie'),
     ('Snowy', 'fox terrier')]



### Select the name, age, and hungry columns for hungry dogs between the ages of two and seven.  This query should also list these dogs in alphabetical order.


```python
#Your code here
cur.execute('''select name, age, hungry from dogs where hungry = 1 and age >= 2 and age <= 7 order by name''').fetchall()
```




    [(None, 4, 1),
     ('Clifford', 4, 1),
     ('Lassie', 7, 1),
     ('Scooby', 6, 1),
     ('Snoopy', 3, 1)]



## Summary

Great work! In this lab you practiced writing more complex SQL statements to not only query specific information but also define the quantity and order of your results. 
