Keep stock for Eloquent models. This package will track stock mutations for your models. You can increase, decrease, clear and set stock. It's also possible to check if a model is in stock (on a certain date/time).

## Installation

You can install the package via composer:

``` bash
composer require appstract/laravel-stock
```

By running `php artisan vendor:publish --provider="Appstract\Stock\StockServiceProvider"` in your project all files for this package will be published. Run `php artisan migrate` to migrate the table. There will now be a `stock_mutations` table in your database.

## Usage

Adding the `HasStock` trait will enable stock functionality on the Model.

``` php
use Appstract\Stock\HasStock;

class Book extends Model
{
    use HasStock;
}
```

### Basic mutations

```php
$book->increaseStock(10);
$book->decreaseStock(10);
$book->mutateStock(10);
$book->mutateStock(-10);
```

### Clearing stock

It's also possible to clear the stock and directly setting a new value.

```php
$book->clearStock();
$book->clearStock(10);
```

### Setting stock

It is possible to set stock. This will create a new mutation with the difference between the old and new value.

```php
$book->setStock(10);
```

### Check if model is in stock

It's also possible to check if a product is in stock (with a minimal value).

```php
$book->inStock();
$book->inStock(10);
```

### Current stock

Get the current stock value (on a certain date).

```php
$book->stock;
$book->stock(Carbon::now()->subDays(10));
```

### Stock arguments

Add a description and/or reference model to de StockMutation.

```php
$book->increaseStock(10, [
    'description' => 'This is a description',
    'reference' => $otherModel,
]);
```

### Query Scopes

It is also possible to query based on stock.

```php
Book::whereInStock()->get();
Book::whereOutOfStock()->get();
```

## Testing

``` bash
composer test
```
