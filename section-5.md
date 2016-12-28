# Section 5: Common Request

## Setup Multilingual

You can setup multilingual by configure `config/app.php`'s `locale` key or you may call `App::setLocale('my')` at run time.

Then make sure the language set is exist by duplicate the `resources/lang/en` to `resources/lang/xx`.

## Setup Validation Messages

Open up your `resources/lang/xx/validation.php` and update your key's values based on your language.