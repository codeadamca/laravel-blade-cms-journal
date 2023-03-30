# Journal Module for Laravel CMS

This is a basic journal module basaed on the Laravel CMS avalable in my [laravel-blade-cms](https://github.com/codeadamca/laravel-blade-cms) repo.

## Database

Before we start coding the list, add, edit, and delete files, we need a table to store our journal entries. Creating a table with testing data requires us to create a migration, model, factory, and add some instructions to our seeding script. 

### Migrations

Before we make any files, use the Terminal to change the working directory to your project directory. I am using a Mac and my project folder was on my desktop:

``` sh
cd ~
cd Desktop
cd laravel-blade-cms
```

1. Using the Laravel Artisan tool, create a new migration file:

    ```sh
    php artisan make:migration create_entries_table
    ```
    
    You will now have a new migration file named `<YEAR>_<MONTH>_<DAY>_<SECONDS>_create_entries_table.php`.
    
    
    > **Note** 
    > Laravel uses a database naming convention named [Eloquent](https://laravel.com/docs/10.x/eloquent). Eloquent states that tables names are lowercase and plural.  

2. In the new migration file, change the schema to:

    ```php
    Schema::create('entries', function (Blueprint $table) {
        $table->id();

        $table->string('title');
        $table->text('content');

        $table->timestamp('learned_at');

        $table->timestamps();
    });
    ```
    
### Model

We need a new model to define the `entries` table relationships and rules. The model scaffolding that Artisan provides is sufficient.

1. Create a new `Entry` model: 

    ```sh
    php artisan make:model Endry
    ```
    
2. You will now have a filed named `Entry.php` in the `/app/Models` folder. No changes needed.
    
### Factory

We need a factory to give Laravel instructions on how to populate the factory table. 

1. Creat a new factory:

    ```sh
    php artisan make:factory EntryFactory
    ```
    
2. You will now have a filed named `EntryFactory.php` in the `/database/factories` folder. Open this faile and change the definiation method retrn value to:

    ```php
    return [
        'title' => $this->faker->sentence,
        'content' => $this->faker->paragraph,
        'learned_at' => $this->faker->dateTimeThisMonth,
    ];
    ```
    
### Seeding

Lastly we need to give Laravel instructions on how many entries to add. 

1. Open up the `DatabaseSeeder.php` file in the `/database/seeders` folder.

2. At the top of the file add the entries model, add this line below `use App\ModelProject;`:

    ```php
    use App\Models\Entry;
    ```
    
3. Add some code to remove existing records when seeding it initiated. Add this below `Project::truncate();`:

    ```php
    Entry::truncate();
    ```
    
4. Add code to add four fake entries. Add this line under `Project::factory()->count(4)->create();`:

    ```php
    Entry::factory()->count(4)->create();
    ```
    
### Execute
    
Lastly we need to execute our migrations and seeding. Using the Terminal (or GitBash on a Windows machine) run this comment:

```sh
php artisan migrate:fresh --seed
```

![Migrate and Seed](https://raw.githubusercontent.com/codeadamca/laravel-blade-cms-journal/main/_readme/screenshot-migrate-seed.png)

If you received no errors, there will be tables with data in your database. OPen up phpMyAdmin to check!

![Entries Table](https://raw.githubusercontent.com/codeadamca/laravel-blade-cms-journal/main/_readme/screenshot-entries.png)

## List, Add, Edit and Delete

Now that the database is ready and poulated, we need to create the list, add, edit, and delete code. Let's start by adding the list.

### Dashboard

Open up `dashboard.blade.php` in the `resources/views/console/` folder, and add link to manage entries. Add this line after types.

```php
<li><a href="/console/entries/list">Manage Journal Entries</a></li>
```

Open a browser, login to the CMS, and click `Manage Journal Entries`. You should get a `page not found` error. We need to add some new routes.

SCREENSHOT PAGE NOT FOUND

### Routes

Open the `web.php` file in the routes folder. Import the `EntriesController` by adding a `use` command to the top of your file.

```php
use App\Http\Controllers\EntriesController;
```

Copy and paste one of the list routes from one of the other modules and update for `entries`.

```php
Route::get('/console/entries/list', [EntriesController::class, 'list'])->middleware('auth');
```

Refresh your browser, and you will get a new error message that states `EntriesController does not exist`.

SCREENSHOT CONT DOES NOT EXIST

### Controller



   
***

## Repository Resources

* [laravel-blade-cms](https://github.com/codeadamca/laravel-blade-cms)
* [Laravel](https://laravel.com/)

<a href="https://codeadam.ca">
<img src="https://codeadam.ca/images/code-block.png" width="100">
</a>
