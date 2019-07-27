This package is based on "spatie/laravel-query-builder" allows you to rapidly creating API controllers for your Laravel application. This package also works with authorization policies.

## Basic Usage

Create a new table seeder class: `php artisan make:seeder ProductsTableSeeder` and change the content to following code. The csv file must located in `/database/seeds/csvs/products.csv`

```php
use \DevLabor\CsvSeeder\Database\Seeder\CsvSeeder

// ...

class ProductsTableSeeder extends CsvSeeder {
/**
 * UsersTableSeeder constructor.
 */
public function __construct()
{
	$this->columnMapping = [
		0 => 'article_no',
		1 => 'name',
		2 => 'text',
		3 => 'price'
	];
}

/**
 * Run the database seeds.
 *
 * @return void
 */
public function run()
{
	// Recommended when importing larger CSVs
	\Illuminate\Support\Facades\DB::disableQueryLog();

	// Uncomment the below to wipe the table clean before populating
	\Illuminate\Support\Facades\DB::table($this->guessTableName())->truncate();

	parent::run();
}
}
```

## Installation

You can install the package via composer:

```bash
composer require devlabor/csv-seeder
```

## Usage

This CsvSeeder class is easy to use and usually works independently. Sometimes you need or want to customize the csv import file parameters.

### Parameters

```php
// Database table name for seeding. Default guessed by class name.
public $table = '';
```

```php
// CSV file name for seeding. Default guessed by class name.
public $filename = '';
```

```php
// DB field that to be hashed, most likely a password field. If your password has a different name, please overload this variable from our seeder class.
public $hashable = 'password';
```

```php
// An SQL INSERT query will execute every time this number of rows are read from the CSV. Without this, large INSERTS will silently fail.
public $insertChunkSize = 50;
```

```php
// CSV delimiter (defaults to ;)
public $csvDelimiter = ';';
```

```php
// Number of rows to skip at the start of the CSV
public $offsetRows = 0;
```

```php
// Can be used to tell the import to trim any leading or trailing white space from the column;
public $trimWhitespace = true;
```

```php
/**
 * The mapping of CSV to DB column. If not specified manually, the first row (after $offsetRows) of your CSV will be read as your table columns.
 *
 * In order to read the first, third and fourth columns of your CSV only, use:
 * array(
 *   0 => id,
 *   2 => name,
 *   3 => description,
 * )
 */
public $columnMapping = [];
```

### Testing

```bash
composer test
```

### Security

If you discover any security related issues, please email office@devlabor.com instead of using the issue tracker.

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.