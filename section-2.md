# Section 2: How to create a page

## Route

Set Route - `routes/web.php`

```php
Route::get('about-us','PageController@aboutUs')
```

## Controller

Create a controller - `php artisan make:controller PageController --resource` - and create a method `aboutUs` returning view from `pages.index`.

```php
public function aboutUs()
{
	return view('pages.index');
}
```

## View

Create the view - create new folder in `resources/views/` named `pages`. In `pages`, create `aboutUs.blade.php`. Add the following content:

```html
@extends('layouts.app')

@section('content')
<div class="container">
    <div class="row">
		<h1>About Us</h1>
    </div>
</div>
@endsection
```