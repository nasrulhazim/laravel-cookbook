# Section 4: Relationship

1. One-to-one
2. One-to-many
3. Many-to-one
4. Many-to-many

You may have following relationships between your models, but following are the 3 basic steps required to setup relationship between tables.

## Setup Foreign Key

Let say we want to have a user has many posts.

Create migration script:

```
php artisan make:migration add_post_owner --table=posts
```

Open up the `timestamp_add_post_owner.php` migration script and add the following in `up` and `down` method respectively.

```
Schema::table('posts', function (Blueprint $table) {
    $table->integer('user_id')->unsigned()->after('id');
});
```

Using `after('column_name')` used, in order to prevent the new column added at the end of the table columns.

```
Schema::table('posts', function (Blueprint $table) {
    $table->dropColumn('user_id');
});
```

Then we run `php artisan migrate`.

## Update `ModelFactory.php`

Update the `App\Post` model factory by adding `user_id`.

```
$factory->define(App\Post::class, function (Faker\Generator $faker) {
    return [
        'user_id' => $faker->randomElement(range(1, 100)),
        'post' => $faker->paragraph,
    ];
});
```

## Define Relationships in Models

Next we need to add relationship between related models, in this case we need `User` and `Post` model.

For `User` model, a user has many posts, add the following method `app/User.php`:

```php
public function posts()
{
    return $this->hasMany('App\Post');
}
```

For `Post` model, a post belongs to user, add the following method `app/Post.php`:

```php
public function user()
{
    return $this->belongsTo('App\User');
}
```

## Usage 

Once you're done setting up the relationships, you may use the models like:

```php
$user = User::find(1);
// just dump all the posts
dd($user->posts);
```

```php
$post = Post::find(1);
// echo the owner of the post
$post->user->name;
```