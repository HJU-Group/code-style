# Testing

## PHPUnit

### General

A file should be created for each class being tested or where tests should
logically be combined.

#### Code

Any repeated code in tests should be pulled into its own method whenever possible.

If it is something that is shared across multiple tests such as an action or service class
it should be created in the setUp method and assigned to a public variable.

##### Example

```php
class UpdateUserContactSettingsTest extends TestCase
{
    use DatabaseMigrations, SeedDatabaseAfterRefresh;

    /**
     * @var UpdateUserContactSettings
     */
    public $service;

    public function setUp()
    {
        parent::setUp();

        $this->service = app(UpdateUserContactSettings::class);
    }

    /**
     * @test
     * @covers \App\Actions\User\UpdateUserContactSettings::execute
     */
    public function valid_data()
    {
        $user = factory(User::class)->create();
        $data = [
            'email' => 'test@test.com',
            'phone' => '5555555555',
        ];

        $this->service->execute($user, $data);
        $user->refresh();

        $this->assertEquals($data, [
            'email' => $user->email,
            'phone' => $user->phone,
        ]);
    }
}
```

#### Structure

Test should start with setup, follow by act (what you are testing),
and then assertion(s).

A test must contain at least 1 assertion.

##### Example

```php
/** @test */
function user_setting_service_can_update_phone_number()
{   
    $phone = '555-555-5555';
    
    $this->service->updatePhoneNumber([
        'phone' => $phone,
    ]);
    
    $this->assertDatabaseHas('user_settings', [
        'phone' => $phone,
    ]);
}
```

#### Names

Should be clear and concise, use the test doc block, and should include @covers

##### Bad:

```php
function test_new_user()
{
    ...
}
```

##### Good:

```php
/** @test */
function user_can_register_sucessfully()
{
    ...
}

/** 
 * @test
 * @covers UserSettings::updateEmail
 */
function user_setting_service_can_update_email()
{
    $email = 'test@test.com';
    
    $this->service->updateEmail([
        'email' => $email,
    ]);
    
    $this->assertDatabaseHas('user_settings', [
        'email' => $email,
    ]);
}
```

#### Negative Tests

When possible and reasonable, separate tests should be created to test
for possible negative effects or invalid input.

For example, a user cannot register using a bad email address, or a
method throws an exception when bad data is passed in.

A good rule is if you have to add an exception to your code, you should test
that it can be triggered.

### Unit Tests

#### Size

Unit test should only test one piece of code and for one result.

##### Bad:

```php
/** @test */
function user_setting_service()
{
    $service = app(UserSettingsService);
    
    $service->updatePhoneNumber([
        'phone' => '555-555-5555',
    ]);
    
    $service->updateEmail([
        'email' => 'test@test.com',
    ]);
    
    $this->assertDatabaseHas('user_settings', [
        'phone' => '555-555-5555',
    ]);
    
    $this->assertDatabaseHas('user_settings', [
        'email' => 'test@test.com',
    ]);
}
```

##### Good:

```php
function setUp()
{
    $this->service = app(UserSettingsService);
}

/** 
 * @test
 * @covers \App\Services\UserSettingsService::updatePhoneNumber
 */
function user_setting_service_can_update_phone_number()
{   
    $phone = '555-555-5555';
    
    $this->service->updatePhoneNumber([
        'phone' => $phone,
    ]);
    
    $this->assertDatabaseHas('user_settings', [
        'phone' => $phone,
    ]);
}

/** 
 * @test 
 * @covers \App\Services\UserSettingsService::updateEmail
 */
function user_setting_service_can_update_email()
{
    $email = 'test@test.com';
    
    $this->service->updateEmail([
        'email' => $email,
    ]);
    
    $this->assertDatabaseHas('user_settings', [
        'email' => $email,
    ]);
}
```

### Functional Tests

Functional tests are an end to end test.  They can include hitting API/HTTP end points.

For example, new user registration or updating settings.

### Dusk Tests

These tests should be the final tests created.
