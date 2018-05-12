# PHP

## <a name="variables"></a>Variables / Class properties 

### Must be camelCase

#### Bad:

```php
$server_ip_address = $this->getServerIPAddress();

public function getExtendedAttributes($current_user)
```

#### Good

```php
$serverIPAddress = $this->getServerIPAddress();

public function getExtendedAttributes($currentUser)
```

### Use clear, meaningful, and pronounceable variable names

#### Bad:

```php
$address = $this->getServerIPAddress();

$i = count($sites);
```

#### Good

```php
$serverIPAddress = $this->getServerIPAddress();

$totalSites = count($sites);
```

### Must not be prefixed by their accessbility

#### Bad:

```php
private $_currentUser;

protected $_site;
```

#### Good

```php
private $currentUser;

protected $site;
```

## <a name="functions"></a>Functions / Class Methods

### Must be camelCase

#### Bad:

```php
public function ExtendedAttributes($currentUser)

private function _clean_data_from_system()
```

#### Good

```php
public function getExtendedAttributes($currentUser)

private function cleanDataFromSystem()
```

### Where it makes sense names should be prefixed by a verb

* get
* set
* update
* delete
* fetch

#### Bad:

```php
public function ExtendedAttributes($currentUser)

private function UserDelete($user)
```

#### Good

```php
public function getExtendedAttributes($currentUser)

private function deleteUser($user)
```

### Should not contain un-needed or repetitive words

#### Bad:

```php
Class UserExport 
{
	public function exportUser($user)
	{
	}
}
```

#### Good

```php
Class UserExport
{
	public function export($user)
	{
	}
}
```

## <a name="classes"></a>Classes

### Names should be clear and meaning full

#### Bad:

```php
Class Export 
{
	public function exportUser($user)
	{
	}
}
```

#### Good

```php
Class UserExportServices 
{
	public function export($user)
	{
	}
}
```
