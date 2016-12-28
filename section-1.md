# Section 1: Data Preparation

## Create Model & Migration Script

Run following command in terminal:

```
php artisan make:model Post -m
```

This will create a model named `Post.php` in `app` folder and a migration script `timestamp_create_posts_table.php` in `database\migrations` folder.

## Setup Migration Script Schema

Open up your `timestamp_create_posts_table.php` in `database\migrations` folder and update the schema accordingly.

```php
Schema::create('posts', function (Blueprint $table) {
    $table->increments('id');
    $table->string('post');
    $table->timestamps();
});
```

Read more about [Creating Columns](https://laravel.com/docs/5.3/migrations#creating-columns)

## Setup Fillable

In order to user `Post::create()` method, you need to define the `$fillable` property of the model class.

```php
protected $fillable = [
    'post',
];
```

## Run Migration Scripts

Run the following command to check the migration status:

```
php artisan migrate:status
```

If there's still `N` status, you can run the following command to run the migration scripts.

```
php artisan migrate
```

## Setup Factory

Where you define your data format, how it should be inserted when calling it from `factory()` helper.

```php
$factory->define(App\Post::class, function (Faker\Generator $faker) {
    return [
        'post' => $faker->sentence,
    ];
});
```

## Setup Seeder

Create a seeder file using following command:

```php
php artisan make:seeder PostTableSeeder
```

Open `PostTableSeeder.php` located at `database\seeds` folder and call the factory for `Post`, as following in `run` method:

```php
factory(\App\Post::class, 100)->create();
```

### How to Seed Data

There's three ways in seeding data.

#### Method 1

Following command will seed data by calling `DatabaseSeeder.php`:

```
php artisan db:seed
```

#### Method 2

Following command will seed data by calling seeder class name:

```
php artisan db:seed --class=PostSeeder
```

#### Method 3

Following command will seed data after do the migration:

```
php artisan migrate --seed
```

