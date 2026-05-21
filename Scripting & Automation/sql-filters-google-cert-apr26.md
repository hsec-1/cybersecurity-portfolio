# Apply Filters to SQL Queries — Google Cybersecurity Certificate

## Overview

Applied SQL filters to retrieve and analyse security-relevant data from a database environment. The scenarios simulate real-world data manipulation tasks that a security analyst may be required to perform, ranging from identifying suspicious login attempts to identifying machines requiring updates by department.

---

## Retrieve After Hours Failed Login Attempts

**Scenario:** A potential security incident occurred after business hours. Query the `log_in_attempts` table to identify all failed login attempts that occurred after 18:00.

**Solution:** SELECT all columns from the `log_in_attempts` table. Use the `WHERE` clause and the `AND` operator to select all unsuccessful (`success = FALSE`) login attempts with a time after 18:00 (`login_time > '18:00:00'`).

**Note:** In a real scenario, this time range should also include login attempts after midnight but before normal business hours.

```
MariaDB [organization]> SELECT *
    -> FROM log_in_attempts
    -> WHERE success = FALSE AND login_time > '18:00:00';
+----------+----------+------------+------------+---------+-------------------+---------+
| event_id | username | login_date | login_time | country | ip_address        | success |
+----------+----------+------------+------------+---------+-------------------+---------+
|        2 | apatel   | 2022-05-10 | 20:27:27   | CAN     | 192.168.205.12    |       0 |
|       18 | pwashing | 2022-05-11 | 19:28:50   | US      | 192.168.66.142    |       0 |
|       20 | tshah    | 2022-05-12 | 18:56:36   | MEXICO  | 192.168.109.50    |       0 |
|       28 | aestrada | 2022-05-09 | 19:28:12   | MEXICO  | 192.168.27.57     |       0 |
|       34 | drosas   | 2022-05-11 | 21:02:04   | US      | 192.168.45.93     |       0 |
|       42 | cgriffin | 2022-05-09 | 23:04:05   | US      | 192.168.4.157     |       0 |
+----------+----------+------------+------------+---------+-------------------+---------+
```

---

## Retrieve Login Attempts on Specific Dates

**Scenario:** A suspicious event occurred on 2022-05-09. Review all login attempts on this day and the day before.

**Solution:** SELECT all columns from the `log_in_attempts` table. Use the `WHERE` clause and the `OR` operator to select two dates (`login_date = '2022-05-09' OR login_date = '2022-05-08'`). The `OR` operator combines results from both dates into a single list.

```
MariaDB [organization]> SELECT *
    -> FROM log_in_attempts
    -> WHERE login_date = '2022-05-09' OR login_date = '2022-05-08';
+----------+----------+------------+------------+---------+-------------------+---------+
| event_id | username | login_date | login_time | country | ip_address        | success |
+----------+----------+------------+------------+---------+-------------------+---------+
|        1 | jrafael  | 2022-05-09 | 04:56:27   | CAN     | 192.168.243.140   |       1 |
|        3 | dkot     | 2022-05-09 | 06:47:41   | USA     | 192.168.151.162   |       1 |
|        4 | dkot     | 2022-05-08 | 02:00:39   | USA     | 192.168.178.71    |       0 |
|        8 | bisles   | 2022-05-08 | 01:30:17   | US      | 192.168.119.173   |       0 |
|       12 | dkot     | 2022-05-08 | 09:11:34   | USA     | 192.168.100.158   |       1 |
|       15 | lyamamot | 2022-05-09 | 17:17:26   | USA     | 192.168.183.51    |       0 |
+----------+----------+------------+------------+---------+-------------------+---------+
```

---

## Retrieve Login Attempts Outside of Mexico

**Scenario:** Suspicious login activity has been identified, but the team has determined it did not originate in Mexico. Query all login attempts that occurred outside of Mexico.

**Solution:** SELECT all columns from the `log_in_attempts` table. Use the `WHERE` clause, the `NOT` operator and the `LIKE` operator (`NOT country LIKE 'MEX%'`) to exclude all results from Mexico. The `LIKE` operator with the `%` wildcard was necessary as the database contained multiple formats for Mexico (both `MEX` and `MEXICO`).

```
MariaDB [organization]> SELECT *
    -> FROM log_in_attempts
    -> WHERE NOT country LIKE 'MEX%';
+----------+----------+------------+------------+---------+-------------------+---------+
| event_id | username | login_date | login_time | country | ip_address        | success |
+----------+----------+------------+------------+---------+-------------------+---------+
|        1 | jrafael  | 2022-05-09 | 04:56:27   | CAN     | 192.168.243.140   |       1 |
|        2 | apatel   | 2022-05-10 | 20:27:27   | CAN     | 192.168.205.12    |       0 |
|        3 | dkot     | 2022-05-09 | 06:47:41   | USA     | 192.168.151.162   |       1 |
|        4 | dkot     | 2022-05-08 | 02:00:39   | USA     | 192.168.178.71    |       0 |
|        5 | jrafael  | 2022-05-11 | 03:05:59   | CANADA  | 192.168.86.232    |       0 |
|        7 | eraab    | 2022-05-11 | 01:45:14   | CAN     | 192.168.170.243   |       1 |
+----------+----------+------------+------------+---------+-------------------+---------+
```

---

## Retrieve Employees in Marketing

**Scenario:** Security updates are required on machines in the Marketing department across all East building offices. Query the `employees` table to identify these machines.

**Solution:** SELECT all columns from the `employees` table. Use `WHERE`, `AND` and `LIKE` to filter by department (`department = 'Marketing'`) and East building offices (`office LIKE 'EAST%'`) to account for all office numbers within the East building.

```
MariaDB [organization]> SELECT *
    -> FROM employees
    -> WHERE department = 'Marketing' AND office LIKE 'EAST%';
+-------------+----------------+----------+------------+----------+
| employee_id | device_id      | username | department | office   |
+-------------+----------------+----------+------------+----------+
|        1000 | a320b137c219   | elarson  | Marketing  | East-170 |
|        1052 | a192b174c940   | jdarosa  | Marketing  | East-195 |
|        1075 | x573y883z772   | fbautist | Marketing  | East-267 |
|        1088 | k8651965m233   | rgosh    | Marketing  | East-157 |
|        1103 | NULL           | randerss | Marketing  | East-460 |
|        1156 | a184b775c707   | dellery  | Marketing  | East-417 |
+-------------+----------------+----------+------------+----------+

```

---

## Retrieve Employees in Finance or Sales

**Scenario:** A different security update is required on machines for employees in the Sales and Finance departments.

**Solution:** SELECT all columns from the `employees` table. Use `WHERE` and the `OR` operator to filter to Finance (`department = 'Finance'`) or Sales (`department = 'Sales'`).

**Note:** In normal English, this would be described as a list of Finance *and* Sales staff. However, using the `AND` operator in SQL would return only employees who are members of both departments simultaneously — which is not the intended result.

```
MariaDB [organization]> SELECT *
    -> FROM employees
    -> WHERE department = 'Finance' OR department = 'Sales';
+-------------+----------------+----------+------------+-----------+
| employee_id | device_id      | username | department | office    |
+-------------+----------------+----------+------------+-----------+
|        1003 | d394e816f943   | sgilmore | Finance    | South-153 |
|        1007 | h174i497j413   | wjaffrey | Finance    | North-406 |
|        1008 | i858j583k571   | abernard | Finance    | South-170 |
|        1009 | NULL           | lrodriqu | Sales      | South-134 |
|        1010 | k2421212m542   | jlansky  | Finance    | South-109 |
|        1011 | 1748m120n401   | drosas   | Sales      | South-292 |
+-------------+----------------+----------+------------+-----------+
```

---

## Retrieve All Employees Not in IT

**Scenario:** A security update is needed for all employees except those in the Information Technology department, who have already received it.

**Solution:** SELECT all columns from the `employees` table. Use the `WHERE` clause and the `NOT` operator to exclude IT department employees (`NOT department = 'Information Technology'`).

**Note:** An equivalent query using the `!=` operator: `WHERE department != 'Information Technology'`

```
MariaDB [organization]> SELECT *
    -> FROM employees
    -> WHERE NOT department = 'Information Technology';
+-------------+----------------+----------+-----------------+--------------+
| employee_id | device_id      | username | department      | office       |
+-------------+----------------+----------+-----------------+--------------+
|        1000 | a320b137c219   | elarson  | Marketing       | East-170     |
|        1001 | b239c825d303   | bmoreno  | Marketing       | Central-276  |
|        1002 | c116d593e558   | tshah    | Human Resources | North-434    |
|        1003 | d394e816f943   | sgilmore | Finance         | South-153    |
|        1004 | e218f877g788   | eraab    | Human Resources | South-127    |
|        1005 | f551g340h864   | gesparza | Human Resources | South-366    |
+-------------+----------------+----------+-----------------+--------------+
```

---

## Summary

SQL filters were applied using `AND`, `OR` and `NOT` operators alongside the `LIKE` operator and the `%` wildcard to filter data by patterns, dates, time ranges and strings. These techniques reflect investigative workflows used by security analysts to narrow down relevant data from large datasets.

---

## Skills Demonstrated

`SQL` `Data filtering` `WHERE clause` `Boolean operators` `Pattern matching (LIKE)` `Security log analysis`

---

[← Back to Scripting & Automation](README.md) | [← Back to Portfolio](../README.md)
