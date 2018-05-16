# PHP & Laravel Code Style Guide

Must follow [PSR 1](https://www.php-fig.org/psr/psr-1/) and [PSR 2](https://www.php-fig.org/psr/psr-2/)

## If statements

* Must be wrapped in braces
* Starting brace must be on the same line
* Not operator must be followed by a space
* Should use === whenever possible

### Bad

```php
if ($isAdmin)
    $this->deleteUser($user);

//Another
if (! $isAdmin)
{
    return response('Not authorized');
}
```

### Good

```php
if ($isAdmin) {
    $this->deleteUser($user);
}

if (! $isAdmin) {
    return response('Not authorized');
}

if ($user->id === 1) {
    $this->setAdmin($user);
}
```

## Ternary operators

* The boolean portion must be wrapped with parenthesis
* Each portion should be on its own line

### Bad

```php
$adminID = Auth::user()->isAdmin() ? Auth::user()->admin()->id : null;
```

### Good

```php
$adminID = (Auth::user()->isAdmin()) 
    ? Auth::user()->admin()->id 
    : null;
```

Unless it is short

```php
$color = ($adminID) ? 'red' : 'blue';
```

## Comments

Comments should be avoided.  This should be a code smell.

## Whitespace

* Must be used before final return
* Must be used to allow code to breathe

### Bad

```php
function getPageFooter($pageNumber)
{
    if ($pageNumber == 0) {
        return view('welcome')->render();
    }
    if ($pageNumber != lastPage()) {
        return view('blank')->render();
    }
    $author = getAuthor();
    $author = formatName($author);
    return view('footer')->render();
}
```

### Good

```php
function getPageFooter($pageNumber)
{
    if ($pageNumber == 0) {
        return view('welcome')->render();
    }
    
    if ($pageNumber != lastPage()) {
        return view('blank')->render();
    }
    
    $author = getAuthor();
    $author = formatName($author);
    
    return view('footer')->render();
}
```

## Docblocks

### Example

```php
/**
* @param $user
* @return bool
* @throws Exception
*/
public function isSiteAdmin($user) {
    if (! $this->isAdmin($this)) {
        throw new Exception('Is not Admin');
    }
    
    if ($user->roles() === SITE_ADMIN) {
        return true;
    }
    
    if ($user->id === 1) {
        return true;
    }
    
    return false;
}
```

## Variables / Class properties

* Must be camelCase
* Use clear, meaningful, and pronounceable variable names
* Must not be prefixed by their accessibility

### Bad:

```php
$server_ip_address = $this->getServerIPAddress();
$address = $this->getServerIPAddress();
$i = count($sites);

//Another
private $_currentUser;
```

### Good

```php
$serverIPAddress = $this->getServerIPAddress();
$serverIPAddress = $this->getServerIPAddress();
$totalSites = count($sites);

//Another
private $currentUser;
```

## Functions / Class Methods

* Must be camelCase
* Opening brace must be on its own line
* Scope must not be prefixed by underscore
* Where it makes sense should be prefixed by a verb
    * Names can also be just a verb if it makes sense in the context of the class
    * get
    * set
    * update
    * delete
    * fetch
      * Get remote data
    * is
      * Returns boolean

### Bad:

```php
public function ExtendedAttributes($currentUser)

private function _clean_data_from_system() {
    rmdir('./data');
}

//Another
class UserRights
{
    private function getUserRights()
    private function setUserRights()
}
```

### Good

```php
public function getExtendedAttributes($currentUser)

private function cleanDataFromSystem()
{
    rmdir('./data');
}

//Another
class UserRights
{
    private function get()
    private function set()
}
```

## Classes

* Must be clearly named
* Open brace must be on its own line

### Example

```php
class UserSetting 
{
    public function update($user)
    {
        ...
    }
}
```

### Good

## Arrays

* Each element must be on its own line
* Must use short syntax
* Must have a comma after last element
* Assignment operators must be aligned

### Bad

```php
$colors = array('red', 'blue');

//Another
$colors = [
    'red' => 'FF000', 
    'blue' => '00FF00',
    'green' => '0000FF',
];
```

### Good

```php
$colors = [
    'red', 
    'blue',
];

//Another
$colors = [
    'red'   => 'FF000', 
    'blue'  => '00FF00',
    'green' => '0000FF',
];
```