SQL Injection
Steps to perform SQL Injection:-
1.you need to check whether website is connected to Database or not we will do this by clicking different options in webpage if the url changes or the numbers in the url's are changing then this means website is connected to database.
2.We will check the vulnerability is existed or not we will do this process by inserting a ' after numerical number on the link.
if the page shows no error/page is same then it is secured or if it shows error /page is changed/some changes on the webpage happened then there is a vulnerability. Also as we had performed this test we got to know that this site is using MySQL server. And this site shows error this means that site is vulnerable.
3.We are going to check how many public columns are available we will do this by adding order by 1,2,3 to the end of the URL. We will change the number like 1,2 until we get an error. Suppose we are getting error in nth column then it means that (n-1)th columns are available in public. Here in this site we got error in 12th column that means 11 columns are available in public.  
4. We need to find how many columns are having loop holes/vulnerabilities. We will do this by writing union select 1,2,3,4,5,6,,7,8,9,10,11 after next to the link. If we perform this operation in this site then it shows 2,7,9 are vulnerable.
5.Now we need to find the name of database with vulnerability. We will do this by removing a vulnerable database number in the previous command and entering database() instead of it. As we perform this process in the place of 2 and  we got to know that it's name is acuart. 
6.We need to find the table names from database with vulnerability. We will do this by removing database() in previous command and writing group_concat(table_name) then at the last of the link we will write 'from information_schema.tables where table_schema=database()'.As a result we got to know the table names of the database that are artists,carts,categ,featured,guestbook,pictures,products,users.
7.So here now we will find the columns names from tables. We will replace table with the column. And we will write link as http://testphp.vulnweb.com/listproducts.php?cat=1%20union%20select%201,group_concat(column_name),3,4,5,6,7,8,9,10,11%20from%20information_schema.columns%20where%20table_name=0x7573657273. This will redirect us to the users table of the acuart database.
And will give the following output at the last of the webpage uname,pass,cc,address,email,name,phone,cart.
8.Now to get user name and password from that column name type uname,0x3a,pass under brackets of group concat().And write from users at the end of the link. By performing this operation we are expecting output in the form of username:password.And we get this the username is test and the password is also test.We got output in the format like this =>test:test.
URL is-> http://testphp.vulnweb.com/listproducts.php?cat=1%20union%20select%201,group_concat(uname,0x3a,pass),3,4,5,6,7,8,9,10,11%20from%20users

Mistakes:
1.First mistake is done by Database admin that database is not secured because data base is accepting commands from end user through url.
2.Second the mistake is done by web developer that the page has to redirect to 404 error page if there is a change made in the url.It has to give you that page is not available.
3.System Admin/network Admin has to configure the firewall properly because the website was bypassed by hex decimals.The firewall was not configured properly.
