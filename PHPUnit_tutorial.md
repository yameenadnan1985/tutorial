# PHPUnit
**Good Video**
```
https://www.youtube.com/watch?v=ZtCkSG90mV8
```


**Install PHPUnit**
```
Step 1:
Go to http://phpunit.de and check phpunit version compatible with your PHP version once you find the compatible version copy the composer command and go to root directory or directory containing application directory and run the command.

Example: composer require --dev phpunit/phpunit ^6

To verify if PHPUnit is installed successfully go to your root directory where vendor and application folders are and in command line type /vendor/bin/phpunit -version
It should return the phpunit version

Step 2:
Create "tests" folder inside "applications" folder and

# Setup ci-phpunit-test
Go to this URL
https://github.com/kenjis/ci-phpunit-test/releases

and download it menually, unzip it and go inside test folder and copy and paste all contents from ci-phpunit-test to applications/tests/

once copied go inside test directory and run this command ../../vendor/bin/phpunit and hit enter, you should see test results
```

**How to write tests**
