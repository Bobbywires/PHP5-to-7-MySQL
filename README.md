# PHP5-to-7-MySQL Quick and dirty

Make sure $link or some similar varable is used in all $link = mysql_connect statements and not used for any other purpose 

Using a file editor like Notepad++ perform the following Find and Replace in all .PHP files

Replace  mysql_           with  mysqli_

Replace  mysqli_query($   with  mysqli_query($link,$

Replace  mysqli_query("   with  mysqli_query($link,"

Replace mysqli_error()    with  mysqli_error($link)

Replace mysqli_affected_rows()  with    mysqli_affected_rows($link)

Replace MYSQL_ASSOC        with    MYSQLI_ASSOC  // must be Ucase, This fixes earlier mysql_ with  mysqli_ 
   "     MYSQLI_NUM        with    MYSQLI_NUM
   "     MYSQLI_BOTH       with    MYSQLI_BOTH
 
Replace mysqli_real_escape_string($  with    mysqli_real_escape_string($link,
Replace mysqli_real_escape_string ($  with    mysqli_real_escape_string($link, // because some code has blank after string

mysqli_insert_id()        with    mysqli_insert_id($link)

Add the line:  global $link;   in all functions using the $link variable
Since most applications have one include for the connection to MySQL with code something like:
$link = mysql_connect($SQHost, $SQLuser, $SQLpw)
    or die('Could not connect: ' . mysql_error());
mysql_select_db($SQLdb) or die('Could not select database');

change the following code to something like this:

$link = mysqli_connect($SQHost, $SQLuser, $SQLpw, $SQLdb) // add $SQLdb as the 4th parameter
Remove the mysql_select_db($SQLdb)

I then used https://github.com/Alexia/php7mar  to catch any mistakes

php mar.php -f="c:/inetpub/wwwroot/application directory/"
 
