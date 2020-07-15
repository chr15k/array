# Array helpers for your PHP project

[![Latest Stable Version](https://poser.pugx.org/chr15k/array/v)](//packagist.org/packages/chr15k/array) [![Latest Unstable Version](https://poser.pugx.org/chr15k/array/v/unstable)](//packagist.org/packages/chr15k/array) [![Total Downloads](https://poser.pugx.org/chr15k/array/downloads)](//packagist.org/packages/chr15k/array) [![License](https://poser.pugx.org/chr15k/array/license)](//packagist.org/packages/chr15k/array)

This package provides useful helpers for working with arrays in PHP.

Based on ...

- Laravel's array helper work (https://github.com/laravel/framework)

## Install
You can install this package via composer:

```bash
composer require chr15k/array
```

## Usage

- [accessible](#accessible)
- [add](#add)
- [collapse](#collapse)
- [crossJoin](#crossJoin)
- [divide](#divide)
- [dot](#dot)
- [except](#except)
- [exists](#exists)
- [first](#first)
- [flatten](#flatten)
- [forget](#forget)
- [get](#get)
- [has](#has)
- [hasAny](#hasAny)
- [isAssoc](#isAssoc)
- [isMultiDimensional](#isMultiDimensional)
- [last](#last)
- [only](#only)
- [pluck](#pluck)
- [prepend](#prepend)
- [pull](#pull)
- [query](#query)
- [random](#random)
- [set](#set)
- [shuffle](#shuffle)
- [sort](#sort)
- [sortRecursive](#sortRecursive)
- [where](#where)
- [wrap](#wrap)

### <a id="accessible"></a>Arr::accessible()
The Arr::accessible method checks that the given value is array accessible:

```php
<?php

use Chr15k\Arr\Arr;

$isAccessible = Arr::accessible(['a' => 1, 'b' => 2]);

// true

$isAccessible = Arr::accessible('abc');

// false

$isAccessible = Arr::accessible(new stdClass);

// false
```

### <a id="add"></a>Arr::add()
The Arr::add method adds a given key / value pair to an array if the given key doesn't already exist in the array or is set to null:

```php
<?php

use Chr15k\Arr\Arr;

$array = Arr::add(['name' => 'Desk'], 'price', 100);

// ['name' => 'Desk', 'price' => 100]

$array = Arr::add(['name' => 'Desk', 'price' => null], 'price', 100);

// ['name' => 'Desk', 'price' => 100]
```

### <a id="collapse"></a>Arr::collapse()
The Arr::collapse method collapses an array of arrays into a single array:

```php
<?php

use Chr15k\Arr\Arr;

$array = Arr::collapse([[1, 2, 3], [4, 5, 6], [7, 8, 9]]);

// [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### <a id="crossJoin"></a>Arr::crossJoin()
The Arr::crossJoin method cross joins the given arrays, returning a Cartesian product with all possible permutations:

```php
<?php

use Chr15k\Arr\Arr;

$matrix = Arr::crossJoin([1, 2], ['a', 'b']);

/*
    [
        [1, 'a'],
        [1, 'b'],
        [2, 'a'],
        [2, 'b'],
    ]
*/

$matrix = Arr::crossJoin([1, 2], ['a', 'b'], ['I', 'II']);

/*
    [
        [1, 'a', 'I'],
        [1, 'a', 'II'],
        [1, 'b', 'I'],
        [1, 'b', 'II'],
        [2, 'a', 'I'],
        [2, 'a', 'II'],
        [2, 'b', 'I'],
        [2, 'b', 'II'],
    ]
*/
```

### <a id="divide"></a>Arr::divide()
The Arr::divide method returns two arrays, one containing the keys, and the other containing the values of the given array:

```php
<?php

use Chr15k\Arr\Arr;

[$keys, $values] = Arr::divide(['name' => 'Desk']);

// $keys: ['name']

// $values: ['Desk']
```

### <a id="dot"></a>Arr::dot()
The Arr::dot method flattens a multi-dimensional array into a single level array that uses "dot" notation to indicate depth:

```php
<?php

use Chr15k\Arr\Arr;

$array = ['products' => ['desk' => ['price' => 100]]];

$flattened = Arr::dot($array);

// ['products.desk.price' => 100]
```

### <a id="except"></a>Arr::except()
The Arr::except method removes the given key / value pairs from an array:

```php
<?php

use Chr15k\Arr\Arr;

$array = ['name' => 'Desk', 'price' => 100];

$filtered = Arr::except($array, ['price']);

// ['name' => 'Desk']
```

### <a id="exists"></a>Arr::exists()
The Arr::exists method checks that the given key exists in the provided array:

```php
<?php

use Chr15k\Arr\Arr;

$array = ['name' => 'John Doe', 'age' => 17];

$exists = Arr::exists($array, 'name');

// true

$exists = Arr::exists($array, 'salary');

// false
```

### <a id="first"></a>Arr::first()
The Arr::first method returns the first element of an array passing a given truth test:

```php
<?php

use Chr15k\Arr\Arr;

$array = [100, 200, 300];

$first = Arr::first($array, function ($value, $key) {
    return $value >= 150;
});

// 200


// A default value may also be passed as the third parameter to the method. This value will be returned if no value passes the truth test:

$first = Arr::first($array, $callback, $default);
```

### <a id="flatten"></a>Arr::flatten()
The Arr::flatten method flattens a multi-dimensional array into a single level array:

```php
<?php

use Chr15k\Arr\Arr;

$array = ['name' => 'Joe', 'languages' => ['PHP', 'Ruby']];

$flattened = Arr::flatten($array);

// ['Joe', 'PHP', 'Ruby']
```

### <a id="forget"></a>Arr::forget()
The Arr::forget method removes a given key / value pair from a deeply nested array using "dot" notation:

```php
<?php

use Chr15k\Arr\Arr;

$array = ['products' => ['desk' => ['price' => 100]]];

Arr::forget($array, 'products.desk');

// ['products' => []]
```

### <a id="get"></a>Arr::get()
The Arr::get method retrieves a value from a deeply nested array using "dot" notation:

```php
<?php

use Chr15k\Arr\Arr;

$array = ['products' => ['desk' => ['price' => 100]]];

$price = Arr::get($array, 'products.desk.price');

// 100


// The Arr::get method also accepts a default value, which will be returned if the specific key is not found:

$discount = Arr::get($array, 'products.desk.discount', 0);

// 0
```

### <a id="has"></a>Arr::has()
The Arr::has method checks whether a given item or items exists in an array using "dot" notation:

```php
<?php

use Chr15k\Arr\Arr;

$array = ['product' => ['name' => 'Desk', 'price' => 100]];

$contains = Arr::has($array, 'product.name');

// true

$contains = Arr::has($array, ['product.price', 'product.discount']);

// false
```

### <a id="hasAny"></a>Arr::hasAny()
The Arr::hasAny method checks whether any item in a given set exists in an array using "dot" notation:

```php
<?php

use Chr15k\Arr\Arr;

$array = ['product' => ['name' => 'Desk', 'price' => 100]];

$contains = Arr::hasAny($array, 'product.name');

// true

$contains = Arr::hasAny($array, ['product.name', 'product.discount']);

// true

$contains = Arr::hasAny($array, ['category', 'product.discount']);

// false
```

### <a id="isAssoc"></a>Arr::isAssoc()
The Arr::isAssoc returns true if the given array is an associative array. An array is considered "associative" if it doesn't have sequential numerical keys beginning with zero:

```php
<?php

use Chr15k\Arr\Arr;

$isAssoc = Arr::isAssoc(['product' => ['name' => 'Desk', 'price' => 100]]);

// true

$isAssoc = Arr::isAssoc([1, 2, 3]);

// false
```

### <a id="isMultiDimensional"></a>Arr::isMultiDimensional()
The Arr::isMultiDimensional method returns true if the given array is multi-dimensional

```php
<?php

use Chr15k\Arr\Arr;

$isMultiDimensional = Arr::isMultiDimensional(['product' => ['name' => 'Desk', 'price' => 100]]);

// true

$isMultiDimensional = Arr::isMultiDimensional([2, 3, [4]]);

// true

$isMultiDimensional = Arr::isMultiDimensional([2, 3, 4]);

// false

$isMultiDimensional = Arr::isMultiDimensional(['name' => 'Desk', 'price' => 100]);

// false


// Accounts for empty arrays

$isMultiDimensional = Arr::isMultiDimensional(['name' => 'Desk', 'price' => 100, []]);

// true
```

### <a id="last"></a>Arr::last()
The Arr::last method returns the last element of an array passing a given truth test:

```php
<?php

use Chr15k\Arr\Arr;

$array = [100, 200, 300, 110];

$last = Arr::last($array, function ($value, $key) {
    return $value >= 150;
});

// 300

// A default value may be passed as the third argument to the method. This value will be returned if no value passes the truth test:

$last = Arr::last($array, $callback, $default);
```

### <a id="only"></a>Arr::only()
The Arr::only method returns only the specified key / value pairs from the given array:

```php
<?php

use Chr15k\Arr\Arr;

$array = ['name' => 'Desk', 'price' => 100, 'orders' => 10];

$slice = Arr::only($array, ['name', 'price']);

// ['name' => 'Desk', 'price' => 100]
```

### <a id="pluck"></a>Arr::pluck()
The Arr::pluck method retrieves all of the values for a given key from an array:

```php
<?php

use Chr15k\Arr\Arr;

$array = [
    ['developer' => ['id' => 1, 'name' => 'Taylor']],
    ['developer' => ['id' => 2, 'name' => 'Abigail']],
];

$names = Arr::pluck($array, 'developer.name');

// ['Taylor', 'Abigail']

// You may also specify how you wish the resulting list to be keyed:

$names = Arr::pluck($array, 'developer.name', 'developer.id');

// [1 => 'Taylor', 2 => 'Abigail']
```

### <a id="prepend"></a>Arr::prepend()
The Arr::prepend method will push an item onto the beginning of an array:

```php
<?php

use Chr15k\Arr\Arr;

$array = ['one', 'two', 'three', 'four'];

$array = Arr::prepend($array, 'zero');

// ['zero', 'one', 'two', 'three', 'four']


// If needed, you may specify the key that should be used for the value:

$array = ['price' => 100];

$array = Arr::prepend($array, 'Desk', 'name');

// ['name' => 'Desk', 'price' => 100]
```

### <a id="pull"></a>Arr::pull()
The Arr::pull method returns and removes a key / value pair from an array:

```php
<?php

use Chr15k\Arr\Arr;

$array = ['name' => 'Desk', 'price' => 100];

$name = Arr::pull($array, 'name');

// $name: Desk

// $array: ['price' => 100]


// A default value may be passed as the third argument to the method. This value will be returned if the key doesn't exist:

$value = Arr::pull($array, $key, $default);
```

### <a id="query"></a>Arr::query()
The Arr::query method converts the array into a query string:

```php
<?php

use Chr15k\Arr\Arr;

$array = ['name' => 'Taylor', 'order' => ['column' => 'created_at', 'direction' => 'desc']];

Arr::query($array);

// name=Taylor&order[column]=created_at&order[direction]=desc
```

### <a id="random"></a>Arr::random()
The Arr::random method returns a random value from an array:

```php
<?php

use Chr15k\Arr\Arr;

$array = [1, 2, 3, 4, 5];

$random = Arr::random($array);

// 4 - (retrieved randomly)


// You may also specify the number of items to return as an optional second argument.
// Note that providing this argument will return an array, even if only one item is desired:

$items = Arr::random($array, 2);

// [2, 5] - (retrieved randomly)
```

### <a id="set"></a>Arr::set()
The Arr::set method sets a value within a deeply nested array using "dot" notation:

```php
<?php

use Chr15k\Arr\Arr;

$array = ['products' => ['desk' => ['price' => 100]]];

Arr::set($array, 'products.desk.price', 200);

// ['products' => ['desk' => ['price' => 200]]]
```

### <a id="shuffle"></a>Arr::shuffle()
The Arr::shuffle method randomly shuffles the items in the array:

```php
<?php

use Chr15k\Arr\Arr;

$array = Arr::shuffle([1, 2, 3, 4, 5]);

// [3, 2, 5, 1, 4] - (generated randomly)
```

### <a id="sort"></a>Arr::sort()
The Arr::sort method sorts an array by its values.

```php
<?php

use Chr15k\Arr\Arr;

$array = ['Desk', 'Table', 'Chair'];

$sorted = Arr::sort($array);

// ['Chair', 'Desk', 'Table']


// Reverse the order by passing true to the second argument

$sorted = Arr::sort($array, true);

// ['Table', 'Desk', 'Chair']
```

### <a id="sortRecursive"></a>Arr::sortRecursive()
The Arr::sortRecursive method recursively sorts an array using the sort function for numeric sub=arrays and ksort for associative subarrays:

```php
<?php

use Chr15k\Arr\Arr;

$array = [
    ['Roman', 'Taylor', 'Li'],
    ['PHP', 'Ruby', 'JavaScript'],
    ['one' => 1, 'two' => 2, 'three' => 3],
];

$sorted = Arr::sortRecursive($array);

/*
    [
        ['JavaScript', 'PHP', 'Ruby'],
        ['one' => 1, 'three' => 3, 'two' => 2],
        ['Li', 'Roman', 'Taylor'],
    ]
*/
```

### <a id="where"></a>Arr::where()
The Arr::where method filters an array using the given Closure:

```php
<?php

use Chr15k\Arr\Arr;

$array = [100, '200', 300, '400', 500];

$filtered = Arr::where($array, function ($value, $key) {
    return is_string($value);
});

// [1 => '200', 3 => '400']
```

### <a id="wrap"></a>Arr::wrap()
The Arr::wrap method wraps the given value in an array. If the given value is already an array it will not be changed:

```php
<?php

use Chr15k\Arr\Arr;

$string = 'Laravel';

$array = Arr::wrap($string);

// ['Laravel']

// If the given value is null, an empty array will be returned:

$nothing = null;

$array = Arr::wrap($nothing);

// []
```

## Testing
You can run the tests with:

```
vendor/bin/phpunit
```

## License
The MIT License (MIT). Please see [License File](https://github.com/chr15k/array/blob/master/LICENSE.md) for more information.