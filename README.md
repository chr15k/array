# String helpers for your PHP project

[![Latest Stable Version](https://poser.pugx.org/chr15k/string/v)](//packagist.org/packages/chr15k/string) [![Latest Unstable Version](https://poser.pugx.org/chr15k/string/v/unstable)](//packagist.org/packages/chr15k/string) [![Total Downloads](https://poser.pugx.org/chr15k/string/downloads)](//packagist.org/packages/chr15k/string) [![License](https://poser.pugx.org/chr15k/string/license)](//packagist.org/packages/chr15k/string)

This package provides useful helpers for working with strings in PHP, including UUID and ASCII support.

This library has 3 dependencies:

- [doctrine/inflector](https://github.com/doctrine/inflector) (Plural/Singular word support)
- [ramsey/uuid](https://github.com/ramsey/uuid) (UUID generation support)
- [voku/portable-ascii](https://github.com/voku/portable-ascii) (ASCII support)

Based on ...

- Laravel's string helper work (https://github.com/laravel/framework)

## Install
You can install this package via composer:

```bash
composer require chr15k/string
```

## Usage

- [after](#after)
- [after_last](#after_last)
- [before](#before)
- [camel](#camel)
- [contains](#contains)
- [contains_all](#contains_all)
- [ends_with](#ends_with)
- [finish](#finish)
- [is_ascii](#is_ascii)
- [is_uuid](#is_uuid)
- [kebab](#kebab)
- [length](#length)
- [limit](#limit)
- [lower](#lower)
- [match](#match)
- [ordered_uuid](#ordered_uuid)
- [plural](#plural)
- [possessive](#possessive)
- [random](#random)
- [replace_array](#replace_array)
- [replace_first](#replace_first)
- [replace_last](#replace_last)
- [singular](#singular)
- [slug](#slug)
- [snake](#snake)
- [start](#start)
- [starts_with](#starts_with)
- [studly](#studly)
- [title](#title)
- [ucfirst](#ucfirst)
- [upper](#upper)
- [uuid](#uuid)
- [words](#words)

### <a id="after"></a>str_after()
```php
$slice = str_after('This is my name', 'This is');

// ' my name'
```

### <a id="after_last"></a>str_after_last()
```php
$slice = str_after_last('App\Controllers\Controller', '\\');

// 'Controller'
```

### <a id="before"></a>str_before()
```php
$slice = str_before('This is my name', 'my name');

// 'This is '
```

### <a id="camel"></a>str_camel()
```php
$converted = str_camel('foo_bar')

// fooBar
```

### <a id="contains"></a>str_contains()
```php
$contains = str_contains('This is my name', 'my');

// true
```

### <a id="contains_all"></a>str_contains_all()
```php
$containsAll = str_contains_all('This is my name', ['my', 'name']);

// true
```

### <a id="ends_with"></a>str_ends_with()
```php
$result = str_ends_with('This is my name', 'name');

// true
```

### <a id="finish"></a>str_finish()
```php
$adjusted = str_finish('this/string', '/');

// this/string/

$adjusted = str_finish('this/string/', '/');

// this/string/
```

### <a id="is_ascii"></a>str_is_ascii()
```php
$isAscii = str_is_ascii('Chris');

// true

$isAscii = str_is_ascii('ü');

// false
```

### <a id="is_uuid"></a>str_is_uuid()
```php
$isUuid = str_is_uuid('a0a2a2d2-0b87-4a18-83f2-2529882be2de');

// true

$isUuid = str_is_uuid('chris');

// false
```

### <a id="kebab"></a>str_kebab()
```php
$converted = str_kebab('fooBar');

// foo-bar
```

### <a id="length"></a>str_length()
```php
$length = str_length('Chris');

// 5
```

### <a id="limit"></a>str_limit()
```php
$truncated = str_limit('The quick brown fox jumps over the lazy dog', 20);

// The quick brown fox...
```

### <a id="lower"></a>str_lower()
```php
$lower = str_lower('CHRIS');

// chris
```

### <a id="match"></a>str_match()
```php
$matches = str_match('foo*', 'foobar');

// true

$matches = str_match('baz*', 'foobar');

// false
```

### <a id="ordered_uuid"></a>str_ordered_uuid()
The str_ordered_uuid() method generates a "timestamp first" UUID that may be efficiently stored in an indexed database column.
```php
$orderedUuid = str_ordered_uuid();

// 90f81d6c-b4f6-4b03-a82d-800058a21705
```

### <a id="plural"></a>str_plural()
```php
$plural = str_plural('bus');

// buses

$plural = str_plural('child');

// children


// Pass second argument to retrieve the singular or plural form of the string...

$plural = str_plural('child', 2);

// children

$plural = str_plural('child', 1);

// child
```

### <a id="possessive"></a>str_possessive()
```php
$possessive = str_possessive('Chris');

// Chris'

$possessive = str_possessive('David');

// David's

$possessive = str_possessive('it');

// its
```

### <a id="random"></a>str_random()
```php
$random = str_random(40);

// odkX5tWGo3tb8hlNgdoVPjHxZR8xRzii1uFT1cxa
```

### <a id="replace_array"></a>str_replace_array()
```php
$string = 'The event will take place between ? and ?';

$replaced = str_replace_array('?', ['8:30', '9:00'], $string);

// The event will take place between 8:30 and 9:00
```

### <a id="replace_first"></a>str_replace_first()
```php
$replaced = str_replace_first('the', 'a', 'the quick brown fox jumps over the lazy dog');

// a quick brown fox jumps over the lazy dog
```

### <a id="replace_last"></a>str_replace_last()
```php
$replaced = str_replace_last('the', 'a', 'the quick brown fox jumps over the lazy dog');

// the quick brown fox jumps over a lazy dog
```

### <a id="singular"></a>str_singular()
```php
$singular = str_singular('cars');

// car

$singular = str_singular('children');

// child
```

### <a id="slug"></a>str_slug()
```php
$slug = str_slug('Chris The Coder', '-');

// chris-the-coder
```

### <a id="snake"></a>str_snake()
```php
$converted = str_snake('fooBar');

// foo_bar
```

### <a id="start"></a>str_start()
```php
$adjusted = str_start('this/string', '/');

// /this/string

$adjusted = str_start('/this/string', '/');

// /this/string
```

### <a id="starts_with"></a>str_starts_with()
```php
$result = str_starts_with('This is my name', 'This');

// true
```

### <a id="studly"></a>str_studly()
```php
$converted = str_studly('foo_bar');

// FooBar
```

### <a id="title"></a>str_title()
```php
$converted = str_title('a nice title uses the correct case');

// A Nice Title Uses The Correct Case
```

### <a id="ucfirst"></a>str_ucfirst()
```php
$string = str_ucfirst('foo bar');

// Foo bar
```

### <a id="upper"></a>str_upper()
```php
$string = str_upper('chris');

// CHRIS
```

### <a id="uuid"></a>str_uuid()
```php
$uuid = str_uuid();

// 0b1a9d6f-e2c7-489d-93f9-331108ebc314
```

### <a id="words"></a>str_words()
```php
return str_words('Perfectly balanced, as all things should be.', 3, ' >>>');

// Perfectly balanced, as >>>
```

## Testing
You can run the tests with:

```
vendor/bin/phpunit
```

## License
The MIT License (MIT). Please see [License File](https://github.com/chr15k/string/blob/master/LICENSE.md) for more information.