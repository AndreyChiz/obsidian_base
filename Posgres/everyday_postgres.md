`sudo su - user_name`
`psql -h <hostname> -U <username> -d <database_name>`
`postgres@d4d53467f893:~/data$ psql iam -d belka`

`\dt`: список всех таблиц


`select * from belka_test_table order by id desc limit 10;`: последние 10 строк