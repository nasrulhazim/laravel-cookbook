# Section 6: Advanced Request 

## Middleware

### Register Middleware

Open up `app/Http/Kernel.php` and update any of the `Kernel` class properties, depends on your need.

To register middleware globally, use `$middleware` property.

To register middleware in group, use `$middlewareGroups` property.

To register middleware for route, use `$routeMiddleware` property.

### Middleware Usage

There's two category, one from route and the other one from controller's constructor.

#### From Controller

```php
public function __construct()
{
    $this->middleware('auth');
}
```

#### From Route

##### For Individual Route

```php
Route::get('/contact-us', 'StaticPageController@contactUs')->name('static.contactUs')->middleware('auth');
```

##### For Group Route

```php
Route::group([
    'middleware' => ['auth'],
    'prefix' => 'admin',
], function () {
    Route::resource('users', 'UserController');
    Route::resource('posts', 'PostController');
    Route::resource('media', 'MediumController');
});
```