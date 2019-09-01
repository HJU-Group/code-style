# PHPSTORM

## Config

### Editor
* General
   * Ensure line feed at file end on Save
* Code Style (PHP)
   * Set Predefined Style to PSR1/PSR2
      * ![Predefined Style](https://github.com/cca-bheath/code-style/blob/master/img/predefined-style.png)
   * Tabs
      * Tabs and Indents
        * Leave default
      * Spaces
        * Other
           * After Unary Not (!)
      * Wrapping and Braces
        * Array Initializer: Do not wrap
           * Align Key Value Pairs
     * Blank Lines
       * Leave default
     * Code Conversion
       * Force short declaration
       * Add a comma after last element in multiline array
     * Code Generation
       * Variable Naming Style
         * camelCase
       * Default Visibility
         * public
     * PHPDoc
        * Use fully-qualified class names
* Code Style (Javascript)
   * Indent 4 (All)

### File and Code Templates
* Remove contents in `Includes > PHP File Header`

### Plugins
* Required
  * Laravel Plugin
* Optional
  * LaravelStorm
    * https://plugins.jetbrains.com/plugin/9795-laravelstorm
  * .env file support

### PHPUnit
* Set CLI Interpreter
   * Languages & Frameworks > PHP
   * ![CLI Interpreter](https://github.com/cca-bheath/code-style/blob/master/img/cli-interpreter.png)
* Double check PHPUnit Settings
   * Languages & Frameworks > PHP > Test Frameworks > PHPUnit


## Running Tests
* Test Folder
    * ![Test Folder](https://github.com/cca-bheath/code-style/blob/master/img/test-folder.png)
* Test Class
    * ![Test Class](https://github.com/cca-bheath/code-style/blob/master/img/test-class.png)
* Test Method
    * ![Test Method](https://github.com/cca-bheath/code-style/blob/master/img/test-method.png)

## Optional Setup

### Keyboard Shortcuts
* Run Context Configuration
  * If the cursor is in a test method run that method or all the tests in the file if its outside a method
  * My map is ALT + A
* Run
  * Will run the last test run regardless of cursor location
  * My map is ALT + Z
* Find in all files
  * Shift + Shift (Default)
* Optimize (PHP)
  * Ctrl + Alt + O (Default)
  * Removes all non-used classes
* Format
  * Ctrl + Alt + L (Default)
  * Applies the code style config to the code
  * Also works on selected
* Bookmarks
  * Add/Remove bookmark
     * Ctrl + Shift 1-9 (Default) 
  * Go to bookmark
     * Ctrl + 1-9
### File and Code Templates

#### Blade
Make an empty file with extension .blade.php

#### Laravel Test

```php
<?php

#if (${NAMESPACE})
namespace ${NAMESPACE};
#end

use Illuminate\Foundation\Testing\RefreshDatabase;
use Tests\Support\SeedDatabaseAfterRefresh;
use Tests\TestCase;

class ${NAME} extends TestCase
{
    use RefreshDatabase, SeedDatabaseAfterRefresh;

    /**
     * @var
     */
    //public \$service;

    public function setUp()
    {
        parent::setUp();

        //\$this->service = app();
    }

    /**
     * @test
     * @covers 
     */
    public function first_test()
    {
        
    }
}
```

### Live Templates

### pubft
Create a public function test method

```php
/** 
 * @test
 * @covers 
 */
public function $NAME$($PARAMETERS$)
{
    $END$
}

```

## MISC
* Scroll From Source
   * Displays the location of the file in the directory tree
   * ![Scroll from Source](https://github.com/cca-bheath/code-style/blob/master/img/scroll-from-source.png)

## Open PhpStorm from link in Windows/Linux

https://github.com/aik099/PhpStormProtocol

Fix for linux:
https://github.com/sanduhrs/phpstorm-url-handler/issues/8

## References

* https://murze.be/configuring-phpstorms-code-generation
* https://stitcher.io/blog/phpstorm-performance
