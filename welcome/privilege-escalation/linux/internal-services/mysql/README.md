# mySQL

You need credentials to access this, linpeas wil ltell you if there is no password.&#x20;

Once you have credentials this is how you access it.&#x20;

```
mysql -uroot -p
Password: <passowrd>
```

After this we enumerate databases to see what things we can get out of it.&#x20;

![](../../../../../.gitbook/assets/2022-08-08\_14-49.png)

Take this instance as an example, we were able to get credentials out of a database and then switch users.&#x20;

```
show databases;
use <database-name>;
show tables;
select * from <table-name>;
```

Then if we can't find anything here we go onto enumerate for UDF exploitation.
