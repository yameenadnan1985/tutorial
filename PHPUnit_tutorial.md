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

Example: composer require --dev phpunit/phpunit ^6

To verify if PHPUnit is installed successfully go to your root directory where vendor and application 
folders are and in command line type /vendor/bin/phpunit -version
It should return the phpunit version

Step 2:
Create "tests" folder inside "applications" folder and

# Setup ci-phpunit-test
Go to this URL
https://github.com/kenjis/ci-phpunit-test/releases

and download release v0.16.1, unzip it and go inside ci-phpunit-test-0.16.1/application/tests folder and copy and paste all contents 
from ci-phpunit-test-0.16.1/application/tests/ to applications/tests/

once copied go inside tests directory and run this command 
../../vendor/bin/phpunit and hit enter, you should see test results
```


**How to write tests**
```
Inside tests directory create new file with class name "welcome_test"
Example:
Class  Welcome_test {
  publilic function test_index () {
    // This line sends a get request to index method of welcome controller and get the output
    $output = $this->request('GET', 'welcome/index');
    $this->assertContains ('<title>Welcome to Codeigniter</title>', $output);
  }
}
```


** How to fix "Exception: Serialization of 'Closure' is not allowed"**
```
https://github.com/kenjis/ci-phpunit-test/issues/90
```
