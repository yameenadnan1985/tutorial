# PHPUnit
**Good Video**
```
https://www.youtube.com/watch?v=X9AwbSK7Ero
https://www.youtube.com/watch?v=ZtCkSG90mV8
```


**Install PHPUnit**
```
Step 1:
Go to http://phpunit.de (if you are using php7.0.33 then go to https://phpunit.de/getting-started/phpunit-6.html)
and check phpunit version compatible with your PHP version once you find the compatible 
version copy the composer command and go to root directory or directory containing application directory 
and run the command.

wget -O phpunit https://phar.phpunit.de/phpunit-6.phar
chmod +x phpunit

To verify if PHPUnit is installed successfully type command below
./phpunit --version
and it should give some output

Step 2:
Create "tests" folder inside "applications/schools" folder and go to this URL
https://github.com/kenjis/ci-phpunit-test/releases
and download release v0.16.1, unzip it and go inside ci-phpunit-test-0.16.1/application/tests folder and copy 
and paste all contents from ci-phpunit-test-0.16.1/application/tests/ to applications/schools/tests/

once copied go inside tests directory and run this command 
./phpunit 
and hit enter, you should see test results
```


**How to fix "Exception: Serialization of 'Closure' is not allowed"**
```
open applications/schools/tests/phpunit.xml and change 
backupGlobals="true" to backupGlobals="false"

Further explanation here:
https://github.com/kenjis/ci-phpunit-test/issues/90
https://github.com/kenjis/ci-phpunit-test/tree/v0.6.1
```


**How to write tests**
```
Go inside tests/controllers directory create new file with same name as controller name and append it with name test
Example:
For controller name Dashboard.php, create file (Dashboard_test.php) inside applications/schools/tests/controllers

And create a class "Dashboard_test" which extends "TestCase" like below
class Dashboard_test extends TestCase{
}

For each method of Dashboard.php controller write this
public function test_MethodName() {
}
```
