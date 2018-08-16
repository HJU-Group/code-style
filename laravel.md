# Laravel

Laravel specific coding guidelines

## Controllers

### Must only be used for input and output

Should:
* Take in the request
* Validate
* Pass to a service class for processing
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
       
        app(UserSettingsService)->validate($request->all());
        app(UserSettingsService)->update($request->all());
        
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

## Service Classes

Service classes provide reusable methods for domain logic that is not input/output.

Methods and variables should be public to help with unit testing.

There should be unit tests for all methods.

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
       
        app(UserSettingsServices::class)->update(Auth::user(), [
           'phone_number' => $request->get('phone_number'),
           'zip_code'     => $request->get('zip_code'),
        ]);
                
        return response('complete');
    }
}

class UserSettingsServices
{
    /**
     * @param User $user
     */
    public function update($user, $values)
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

## Models

## Migrations
