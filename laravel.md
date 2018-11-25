# Laravel

Laravel specific coding guidelines

## Routes

### Naming

- Should follow the resource actions
- Should be named
    - Show/index route should be single name
    - Other routes should use . notation (route.method)
- Where practical use prefix grouping

#### Example:

```php
Route::get('settings', 'UserSettings@index')->name('settings');
Route::put('settings', 'UserSettings@update');

Route::prefix('settings')->group(function () {
    Route::get('email/work', 'UserEmailSettings@index')
          ->name('settings.email.work');
    Route::post('email/work', 'UserEmailSettings@index')
          ->name('settings.email.work.create');
    Route::put('email/work', 'UserEmailSettings@index')
          ->name('settings.email.work.update');
});
```


## Controllers

### Must only be used for input and output

Should:
* Take in the request
* Validate request or use [request validation class](laravel.md#form-validation-request-class)
* Pass to a [action class](laravel.md#action-classes) for processing
* Return response

#### Bad

```php
class UserSettings extends Controller
{
    public function post(Request $request)
    {
        $request->validate([
           'phone_number'   => 'required',
           'zip_code'       => 'required',
        ]);
       
        if (! $this->isLocalPhoneNumber($request->get('phone_number')))
        {
            return response('failed', 500);
        }
        if (! $this->isBannedPhoneNumber($request->get('phone_number')))
        {
            return response('failed', 500);
        }
        if (! $this->isValidZipCode($request->get('zip_code')))
        {
            return response('failed', 500);
        }
        
        Auth::user()->update([
            'phone_number' => $request->get('phone_number'),
            'zip_code'     => $request->get('zip_code'),
        ]);
        
        return response('complete');
    }
}
```

#### Good

```php
class UserSettingsController extends Controller
{
    public function post(Request $request)
    {
        $request->validate([
           'phone_number'   => 'required',
           'zip_code'       => 'required',
        ]);
        
        if (! app(isLocalPhoneNumber::class)->execute($request->get('phone_number'))) {
            return response('failed', 500);
        }
        if (! app(isBannedPhoneNumber::class)->execute($request->get('phone_number')))  {
            return response('failed', 500);
        }
        
        if (! app(isValidZipCode::class)->execute($request->get('zip_code'))) {
            return response('failed', 500);
        }
        
        return response('complete');
    }
}
```

#### The exception can be made if the controller is slim

```php
class UserSettingsController extends Controller
{
    public function post(Request $request)
    {
        $request->validate([
           'phone_number'   => 'required',
           'zip_code'       => 'required',
        ]);
       
        Auth::user()->update([
            'phone_number' => $request->get('phone_number'),
            'zip_code'     => $request->get('zip_code'),
        ]);
        
        return response('complete');
    }
}
```

## Action Classes

See [Medium](https://medium.com/@remi_collin/keeping-your-laravel-applications-dry-with-single-action-classes-6a950ec54d1d) Post for more information

- Action classes provide reusable method(s) for domain logic that is not input/output.
- Method(s) and variable(s) should be public to help with unit testing.
- There should be unit tests for all methods.
- Must have an execute method

### Example

```php
class UserSettingsController extends Controller
{
    public function post(Request $request)
    {
        $request->validate([
           'phone_number'   => 'required',
           'zip_code'       => 'required',
        ]);
       
        app(UpdateUserSettings::class)->execute(Auth::user(), [
           'phone_number' => $request->get('phone_number'),
           'zip_code'     => $request->get('zip_code'),
        ]);
                
        return response('complete');
    }
}

class UpdateUserSettings
{
    /**
     * @param User $user
     * @param array $values
     */
    public function execute($user, $values)
    {
        $values['phone_number'] = $this->formatPhoneNumber($values['phone_number']);
        $values['zip_code'] = $this->getExtendedZipCode($values['zip_code']);
        
        $user->update([
            'phone_number' => $values['phone_number'],
             'zip_code'    => $values['zip_code'],
        ]);
    }
}
```

## Form Validation Request Class

See [Laravel Docs](https://laravel.com/docs/5.7/validation#form-request-validation) for more infromation

- Should be used where practical
- Named to match the controller request

### Example

```php
class StoreDepartmentsRequest extends FormRequest
{
    /**
     * Get the validation rules that apply to the request.
     *
     * @return array
     */
    public function rules()
    {
        return [
            'name'        => [
                'required',
                'string',
                'max:255',
                Rule::unique('departments')->ignore($this->getDepartmentId()),
            ],
            'description' => [
                'nullable', 
                'string'
            ],
        ];
    }

    /**
     * @return int|null
     */
    protected function getDepartmentId()
    {
        return ($this->department === null)
            ? null
            : $this->department->id;
    }
}
```

## Models

### Location

Must be in a Models directory and namespaced `namespace App\Models;`

### Guarded

Must only have elements guarded.

Default:
```php
protected $guarded = ['id'];
```

### Casting

Casting should be used for all elements

#### Example

```php
protected $casts = [
    'id'      => 'integer',
    'user_id' => 'integer',
];
```

### Scopes, Accessors & Mutators

Can be included in the model class.  However, if there because a large
number they should be moved to their own trait.

If is usable across multiple models move to trait.

### Full Example

```php
<?php

namespace App\Models;

use Illuminate\Database\Eloquent\Model;

class Crew extends Model
{
    /**
     * The protected attributes
     *
     * @var array
     */
    protected $guarded = ['id'];

    /**
     * @var array
     */
    protected $casts = [
        'id'      => 'integer',
        'user_id' => 'integer',
    ];

    /**
     * Users many to many relationship
     *
     * @return \Illuminate\Database\Eloquent\Relations\HasOne
     */
    public function user()
    {
        return $this->hasOne(User::class, 'id', 'user_id');
    }
}
```

## Migrations

- A unique id column should always be used
- Timestamps should be used where practical
- Down method is optional
    - If used dropIfExists should be used vs drop
- Index and foreign keys should be done after the creation of the column
    - Required for any column where needed
    - onDelete and onUpdate should be used on foreign keys

### Example

```php
class CreateEndorsementsTable extends Migration
{
    /**
     * Run the migrations.
     *
     * @return void
     */
    public function up()
    {
        Schema::create('endorsements', function (Blueprint $table) {
            $table->increments('id');
            $table->unsignedInteger('crew_position_id');
            $table->unsignedInteger('endorsement_request_id');
            $table->datetime('approved_at')
                  ->nullable();
            $table->timestamps();

            $table->foreign('endorsement_request_id')
                  ->references('id')
                  ->on('endorsement_requests')
                  ->onDelete('cascade')
                  ->onUpdate('cascade');

            $table->foreign('crew_position_id')
                  ->references('id')
                  ->on('crew_positions')
                  ->onDelete('cascade')
                  ->onUpdate('cascade');

            $table->index('approved_at');
        });
    }

    /**
     * Reverse the migrations.
     *
     * @return void
     */
    public function down()
    {
        Schema::dropIfExists('endorsements');
    }
}
```

## View Models

See [this blog post](https://stitcher.io/blog/laravel-view-models) for more information

Should be used if more than 2 data items are being passed to the view or there is complex logic.
