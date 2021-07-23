[![Latest Stable Version](https://poser.pugx.org/tarikmanoar/larapoint/v/stable)](https://packagist.org/packages/tarikmanoar/larapoint)
[![Total Downloads](https://poser.pugx.org/tarikmanoar/larapoint/downloads)](https://packagist.org/packages/tarikmanoar/larapoint)
[![Latest Unstable Version](https://poser.pugx.org/tarikmanoar/larapoint/v/unstable)](https://packagist.org/packages/tarikmanoar/larapoint) 
[![License](https://poser.pugx.org/tarikmanoar/larapoint/license)](https://packagist.org/packages/tarikmanoar/pointable)

# Laravel Pointable
Point Transaction system for laravel ^8

## Installation

First, pull in the package through Composer.

```js
composer require tarikmanoar/larapoint
```

And then include the service provider within `app/config/app.php`.

```php
'providers' => [
    Manoar\Pointable\PointableServiceProvider::class
];
```

At last you need to publish and run the migration.
```php
php artisan vendor:publish --provider="Manoar\Pointable\PointableServiceProvider" && php artisan migrate
```

-----

### Setup a Model
```php
<?php

namespace App;

use Manoar\Pointable\Contracts\Pointable;
use Manoar\Pointable\Traits\Pointable as PointableTrait;
use Illuminate\Database\Eloquent\Model;

class User extends Model implements Pointable
{
    use PointableTrait;
}
```

### Add Points
```php
$user = User::first();
$amount = 10; // (Double) Can be a negative value
$message = "The reason for this transaction";

//Optional (if you modify the point_transaction table)
$data = [
    'ref_id' => 'someReferId',
];

$transaction = $user->addPoints($amount,$message,$data);

dd($transaction);
```

### Get Current Points
```php
$user = User::first();
$points = $user->currentPoints();

dd($points);
```

### Get Transactions
```php
$user = User::first();
$user->transactions;

//OR
//$user['transactions'] = $user->transactions(2)->get(); //Get last 2 transactions

dd($user);
```

### Count Transactions
```php
$user = User::first();
$user['transactions_total'] = $user->countTransactions();

dd($user);
```
