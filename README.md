# SQL Murder Mystery 
[SQL Murder Mystery](https://mystery.knightlab.com/)
A crime has taken place and the detective needs your help. The detective gave you the crime scene report, but you somehow lost it. You vaguely remember that the crime was a ​murder​ that occurred sometime on ​Jan.15, 2018​ and that it took place in ​SQL City​. Start by retrieving the corresponding crime scene report from the police department’s database.
![diagram](https://github.com/HanaHrubesova/SQL-Murder-Mystery/blob/main/schema.png)

## Solving the Murder
The clue from the the task description is  *..occurred sometime on ​Jan.15, 2018​ and that it took place in ​SQL City​..* . Start searching in the **crime_scene_report** and filer *date* and *city* and *type*.
``` SQL
SELECT
    *
FROM
    crime_scene_report
WHERE
    city='SQL City'
    AND
TYPE='murder'
AND date='20180115'

```
![results of firs query](https://github.com/HanaHrubesova/SQL-Murder-Mystery/blob/main/step_1.png)

To find the first witness and their description of the murderer.
```SQL
SELECT
    t1.name,
    t1.address_street_name,
    t1.address_number,
    t2.transcript
FROM
    person t1
    LEFT JOIN interview t2 ON t2.person_id=t1.id
WHERE
    address_street_name='Northwestern Dr'
ORDER BY
    address_number DESC
LIMIT
    1
```
![results of second query](https://github.com/HanaHrubesova/SQL-Murder-Mystery/blob/main/step_2.png)
To locate the seconfd witness and their testimony.
```SQL
SELECT
    t1.name,
    t1.address_street_name,
    t1.address_number,
    t2.transcript
FROM
    person t1
    LEFT JOIN interview t2 ON t2.person_id=t1.id
WHERE
    address_street_name='Franklin Ave'
    AND NAME LIKE 'Annabel%'
```
![results of third query](https://github.com/HanaHrubesova/SQL-Murder-Mystery/blob/main/step3.png)