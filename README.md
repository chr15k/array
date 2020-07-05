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
- [cross_join](#cross_join)
- [divide](#divide)
- [dot](#dot)
- [except](#except)
- [exists](#exists)
- [first](#first)
- [flatten](#flatten)
- [forget](#forget)
- [get](#get)
- [has](#has)
- [has_any](#has_any)
- [is_assoc](#is_assoc)
- [last](#last)
- [only](#only)
- [pluck](#pluck)
- [prepend](#prepend)
- [pull](#pull)
- [query](#query)
- [random](#random)
- [set](#set)
- [shuffle](#shuffle)
- [sort_recursive](#sort_recursive)
- [where](#where)
- [wrap](#wrap)

### <a id="accessible"></a>arr_accessible()
The arr_accessible method checks that the given value is array accessible:

```php
$isAccessible = arr_accessible(['a' => 1, 'b' => 2]);

// true

$isAccessible = arr_accessible('abc');

// false

$isAccessible = arr_accessible(new stdClass);

// false
```

### <a id="add"></a>arr_add()
The arr_add method adds a given key / value pair to an array if the given key doesn't already exist in the array or is set to null:

```php
$array = arr_add(['name' => 'Desk'], 'price', 100);

// ['name' => 'Desk', 'price' => 100]

$array = arr_add(['name' => 'Desk', 'price' => null], 'price', 100);

// ['name' => 'Desk', 'price' => 100]
```

### <a id="collapse"></a>arr_collapse()
The arr_collapse method collapses an array of arrays into a single array:

```php
$array = arr_collapse([[1, 2, 3], [4, 5, 6], [7, 8, 9]]);

// [1, 2, 3, 4, 5, 6, 7, 8, 9]
```

### <a id="cross_join"></a>arr_cross_join()
The arr_cross_join method cross joins the given arrays, returning a Cartesian product with all possible permutations:

```php
$matrix = arr_cross_join([1, 2], ['a', 'b']);

/*
    [
        [1, 'a'],
        [1, 'b'],
        [2, 'a'],
        [2, 'b'],
    ]
*/

$matrix = arr_cross_join([1, 2], ['a', 'b'], ['I', 'II']);

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

### <a id="divide"></a>arr_divide()
The arr_divide method returns two arrays, one containing the keys, and the other containing the values of the given array:

```php
[$keys, $values] = arr_divide(['name' => 'Desk']);

// $keys: ['name']

// $values: ['Desk']
```

### <a id="dot"></a>arr_dot()
The arr_dot method flattens a multi-dimensional array into a single level array that uses "dot" notation to indicate depth:

```php
$array = ['products' => ['desk' => ['price' => 100]]];

$flattened = arr_dot($array);

// ['products.desk.price' => 100]
```

### <a id="except"></a>arr_except()
The arr_except method removes the given key / value pairs from an array:

```php
$array = ['name' => 'Desk', 'price' => 100];

$filtered = arr_except($array, ['price']);

// ['name' => 'Desk']
```

### <a id="exists"></a>arr_exists()
The arr_exists method checks that the given key exists in the provided array:

```php
$array = ['name' => 'John Doe', 'age' => 17];

$exists = arr_exists($array, 'name');

// true

$exists = arr_exists($array, 'salary');

// false
```

### <a id="first"></a>arr_first()
The arr_first method returns the first element of an array passing a given truth test:

```php
$array = [100, 200, 300];

$first = arr_first($array, function ($value, $key) {
    return $value >= 150;
});

// 200


// A default value may also be passed as the third parameter to the method. This value will be returned if no value passes the truth test:

$first = arr_first($array, $callback, $default);
```

### <a id="flatten"></a>arr_flatten()
The arr_flatten method flattens a multi-dimensional array into a single level array:

```php
$array = ['name' => 'Joe', 'languages' => ['PHP', 'Ruby']];

$flattened = arr_flatten($array);

// ['Joe', 'PHP', 'Ruby']
```

### <a id="forget"></a>arr_forget()
The arr_forget method removes a given key / value pair from a deeply nested array using "dot" notation:

```php
$array = ['products' => ['desk' => ['price' => 100]]];

arr_forget($array, 'products.desk');

// ['products' => []]
```

### <a id="get"></a>arr_get()
The arr_get method retrieves a value from a deeply nested array using "dot" notation:

```php
$array = ['products' => ['desk' => ['price' => 100]]];

$price = arr_get($array, 'products.desk.price');

// 100


// The arr_get method also accepts a default value, which will be returned if the specific key is not found:

$discount = arr_get($array, 'products.desk.discount', 0);

// 0
```

### <a id="has"></a>arr_has()
The arr_has method checks whether a given item or items exists in an array using "dot" notation:

```php
$array = ['product' => ['name' => 'Desk', 'price' => 100]];

$contains = arr_has($array, 'product.name');

// true

$contains = arr_has($array, ['product.price', 'product.discount']);

// false
```

### <a id="has_any"></a>arr_has_any()
The arr_has_any method checks whether any item in a given set exists in an array using "dot" notation:

```php
$array = ['product' => ['name' => 'Desk', 'price' => 100]];

$contains = arr_has_any($array, 'product.name');

// true

$contains = arr_has_any($array, ['product.name', 'product.discount']);

// true

$contains = arr_has_any($array, ['category', 'product.discount']);

// false
```

### <a id="is_assoc"></a>arr_is_assoc()
The arr_is_assoc returns true if the given array is an associative array. An array is considered "associative" if it doesn't have sequential numerical keys beginning with zero:

```php
$isAssoc = arr_is_assoc(['product' => ['name' => 'Desk', 'price' => 100]]);

// true

$isAssoc = arr_is_assoc([1, 2, 3]);

// false
```

### <a id="last"></a>arr_last()
The arr_last method returns the last element of an array passing a given truth test:

```php
$array = [100, 200, 300, 110];

$last = arr_last($array, function ($value, $key) {
    return $value >= 150;
});

// 300

// A default value may be passed as the third argument to the method. This value will be returned if no value passes the truth test:

$last = arr_last($array, $callback, $default);
```

### <a id="only"></a>arr_only()
The arr_only method returns only the specified key / value pairs from the given array:

```php
$array = ['name' => 'Desk', 'price' => 100, 'orders' => 10];

$slice = arr_only($array, ['name', 'price']);

// ['name' => 'Desk', 'price' => 100]
```

### <a id="pluck"></a>arr_pluck()
The arr_pluck method retrieves all of the values for a given key from an array:

```php
$array = [
    ['developer' => ['id' => 1, 'name' => 'Taylor']],
    ['developer' => ['id' => 2, 'name' => 'Abigail']],
];

$names = arr_pluck($array, 'developer.name');

// ['Taylor', 'Abigail']

// You may also specify how you wish the resulting list to be keyed:

$names = arr_pluck($array, 'developer.name', 'developer.id');

// [1 => 'Taylor', 2 => 'Abigail']
```

### <a id="prepend"></a>arr_prepend()
The arr_prepend method will push an item onto the beginning of an array:

```php
$array = ['one', 'two', 'three', 'four'];

$array = arr_prepend($array, 'zero');

// ['zero', 'one', 'two', 'three', 'four']


// If needed, you may specify the key that should be used for the value:

$array = ['price' => 100];

$array = arr_prepend($array, 'Desk', 'name');

// ['name' => 'Desk', 'price' => 100]
```

### <a id="pull"></a>arr_pull()
The arr_pull method returns and removes a key / value pair from an array:

```php
$array = ['name' => 'Desk', 'price' => 100];

$name = arr_pull($array, 'name');

// $name: Desk

// $array: ['price' => 100]


// A default value may be passed as the third argument to the method. This value will be returned if the key doesn't exist:

$value = arr_pull($array, $key, $default);
```

### <a id="query"></a>arr_query()
The arr_query method converts the array into a query string:

```php
$array = ['name' => 'Taylor', 'order' => ['column' => 'created_at', 'direction' => 'desc']];

arr_query($array);

// name=Taylor&order[column]=created_at&order[direction]=desc
```

### <a id="random"></a>arr_random()
The arr_random method returns a random value from an array:

```php
$array = [1, 2, 3, 4, 5];

$random = arr_random($array);

// 4 - (retrieved randomly)


// You may also specify the number of items to return as an optional second argument.
// Note that providing this argument will return an array, even if only one item is desired:

$items = arr_random($array, 2);

// [2, 5] - (retrieved randomly)
```

### <a id="set"></a>arr_set()
The arr_set method sets a value within a deeply nested array using "dot" notation:

```php
$array = ['products' => ['desk' => ['price' => 100]]];

arr_set($array, 'products.desk.price', 200);

// ['products' => ['desk' => ['price' => 200]]]
```

### <a id="shuffle"></a>arr_shuffle()
The arr_shuffle method randomly shuffles the items in the array:

```php
$array = arr_shuffle([1, 2, 3, 4, 5]);

// [3, 2, 5, 1, 4] - (generated randomly)
```

### <a id="sort_recursive"></a>arr_sort_recursive()
The arr_sort_recursive method recursively sorts an array using the sort function for numeric sub=arrays and ksort for associative subarrays:

```php
$array = [
    ['Roman', 'Taylor', 'Li'],
    ['PHP', 'Ruby', 'JavaScript'],
    ['one' => 1, 'two' => 2, 'three' => 3],
];

$sorted = arr_sort_recursive($array);

/*
    [
        ['JavaScript', 'PHP', 'Ruby'],
        ['one' => 1, 'three' => 3, 'two' => 2],
        ['Li', 'Roman', 'Taylor'],
    ]
*/
```

### <a id="where"></a>arr_where()
The arr_where method filters an array using the given Closure:

```php
$array = [100, '200', 300, '400', 500];

$filtered = arr_where($array, function ($value, $key) {
    return is_string($value);
});

// [1 => '200', 3 => '400']
```

### <a id="wrap"></a>arr_wrap()
The arr_wrap method wraps the given value in an array. If the given value is already an array it will not be changed:

```php
$string = 'Laravel';

$array = arr_wrap($string);

// ['Laravel']

// If the given value is null, an empty array will be returned:

$nothing = null;

$array = arr_wrap($nothing);

// []
```

## Testing
You can run the tests with:

```
vendor/bin/phpunit
```

## License
The MIT License (MIT). Please see [License File](https://github.com/chr15k/array/blob/master/LICENSE.md) for more information.