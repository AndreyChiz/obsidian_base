```hsell
sqlite3 hbfr.base.db
.tables
.mode column
.headers on

SELECT * FROM all_task_data ORDER BY rowid DESC LIMIT 3;
SELECT id, title, tags, price FROM checked_task_data LIMIT 3;

```