# Section 3: Form and Validation

# Form

Basic requirement to create a form

- [ ] Form Element `<form></form>`
- [ ] Action - Form submission to where, basically a URL.
- [ ] Method - HTTP Method Type: `GET`, `POST`, `PUT`, `DELETE`
- [ ] CSRF Token - `{{ csrf_token() }}
- [ ] Method Spoofing - Only for `PUT` and `DELETE`: {{ method_field('PUT') }}

## Create

## Update

## Delete

# How to create a validator

Create custom request by running `php artisan make:request UserRequest`.

Open `UserRequest.php` located at `app/Http/Requests`.

Add validation rules for your form at `rules()` method:

```php
return [
    'name' => 'required|min:6|max:255',
    'email' => 'required|email|max:255|unique:users',
    'password' => 'required|min:6|confirmed',
];
```

Next, include `UserRequest` namespace in `UserController` - `use App\Http\Requests\UserRequest;`. 

Now in `UserController`'s `store(Request $request)` method, replace `store(Request $request)` with `store(UserRequest $request)`.

## To display error message

Following are the sample to display an error message

```html
@if ($errors->has('email'))
    <span class="help-block">
        <strong>{{ $errors->first('email') }}</strong>
    </span>
@endif
```

## Authorization

You may return to `true` in `UserRequest`'s `authorize()` method if there's no particular authorization required.

```php
public function authorize()
{
    return true;
}
```

## Validation from within Controller

```php
$this->validate($request, [
    'name' => 'required|min:6|max:255',
    'password' => 'required|min:6|confirmed',
]);
```