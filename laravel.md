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
class UserSettings extends Controller
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
class UserSettings extends Controller
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

## Models

## Migrations
