# SQL Murder Mystery 
[SQL Murder Mystery](https://mystery.knightlab.com/)
A crime has taken place and the detective needs your help. The detective gave you the crime scene report, but you somehow lost it. You vaguely remember that the crime was a ​murder​ that occurred sometime on ​Jan.15, 2018​ and that it took place in ​SQL City​. Start by retrieving the corresponding crime scene report from the police department’s database.
![diagram]()

## Solvíng the Murder
The clue from the the task description is  *..occurred sometime on ​Jan.15, 2018​ and that it took place in ​SQL City​..* . Start searching in the **crime_scene_report** and filer *date* and *city* and *type*.
```
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
![results of firs query]()