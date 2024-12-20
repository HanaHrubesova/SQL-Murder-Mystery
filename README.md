# SQL Murder Mystery 
[SQL Murder Mystery](https://mystery.knightlab.com/)


A crime has taken place and the detective needs your help. The detective gave you the crime scene report, but you somehow lost it. You vaguely remember that the crime was a ​murder​ that occurred sometime on ​Jan.15, 2018​ and that it took place in ​SQL City​. Start by retrieving the corresponding crime scene report from the police department’s database.
![diagram](https://github.com/HanaHrubesova/SQL-Murder-Mystery/blob/main/pictures/schema.png)

## Solving the Murder
The clue from the task description is that *..occurred sometime on ​Jan.15, 2018​ , and that it took place in ​SQL City​..* . Start searching in the **crime_scene_report** and filer *date* and *city* and *type*.
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
![results of firs query](https://github.com/HanaHrubesova/SQL-Murder-Mystery/blob/main/pictures/step_1.png)

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
    t1.address_street_name='Northwestern Dr'
ORDER BY
    t1.address_number DESC
LIMIT
    1
```
![results of second query](https://github.com/HanaHrubesova/SQL-Murder-Mystery/blob/main/pictures/step_2.png)
To locate the second witness and their testimony.
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
    t1.address_street_name='Franklin Ave'
    AND NAME LIKE 'Annabel%'
```
![results of third query](https://github.com/HanaHrubesova/SQL-Murder-Mystery/blob/main/pictures/step3.png)

From the testimony of Monthy Schapiro and Annabel Miller, it is possible to filter the person matching their description. 
```SQL
SELECT
    t1.name,
    t2.plate_number,
    t3.membership_status,
    t3.id,
    t4.check_in_date
FROM
    person t1
    LEFT JOIN drivers_license t2 ON t1.license_id=t2.id
    LEFT JOIN get_fit_now_member t3 ON t3.person_id=t1.id
    LEFT JOIN get_fit_now_check_in t4 ON t4.membership_id=t3.id
WHERE
    t2.plate_number LIKE '%H42W%'
    AND t3.membership_status='gold'
    AND t3.id LIKE '48Z%'
    AND t4.check_in_date='20180109'
```
![results of fourth query](https://github.com/HanaHrubesova/SQL-Murder-Mystery/blob/main/pictures/step_4.png)

Interestingly, we got the same result with Monthy Schapiro's testimony.

When the name *Jeremy Bowers* is input in the  *solution* table, the answer is :
![Murderer](https://github.com/HanaHrubesova/SQL-Murder-Mystery/blob/main/pictures/murderer.png)


Okay, so the murderer is found, now we need to find a real villain behind the crime. 
The Jeremy Bowers interview transcript:
```SQL
SELECT
    t1.name,
    t2.transcript
FROM
    person t1
    LEFT JOIN interview t2 ON t2.person_id=t1.id
WHERE
    t1.name='Jeremy Bowers'
```
![the villain ](https://github.com/HanaHrubesova/SQL-Murder-Mystery/blob/main/pictures/villain_1.png)

So let's find the described woman 
```SQL
SELECT
    t1.name,
    t2.car_model,
    t2.hair_color,
    t2.height,
    t2.gender,
    t3.date,
    t3.event_name
FROM
    person t1
    LEFT JOIN drivers_license t2 ON t2.id=t1.license_id
    LEFT JOIN facebook_event_checkin t3 ON t3.person_id=t1.id
WHERE
    t2.car_model='Model S'
    AND t2.gender='female'
    AND t3.event_name='SQL Symphony Concert'
```
![the villain finished ](https://github.com/HanaHrubesova/SQL-Murder-Mystery/blob/main/pictures/villain_2.png)

Now when the name *Miranda Priestly* is checked in table **solution** .
![the villain finished ](https://github.com/HanaHrubesova/SQL-Murder-Mystery/blob/main/pictures/result.png)