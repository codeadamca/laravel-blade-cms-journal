# Journal Module for Laravel CMS

This is a basic journal module basaed on the Laravel CMS avalable in my [laravel-blade-cms](https://github.com/codeadamca/laravel-blade-cms) repo.

## Migrations

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
    
## Model

We need a new model to define the `entries` table relationships and rules. The model scaffolding that Artisan provides is sufficient.

1. Create a new `Entry` model: 

    ```sh
    php artisan make:model Endry
    ```
    
2. You will now have a filed named `Entry.php` in the `/app/Models` folder. No changes needed.
    
## Factory

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
    
## Seeding

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
    
## Execute
    
Lastly we need to execute our migrations and seeding. Using the Terminal (or GitBash on a Windows machine) run this comment:

```sh
php artisan migrate:fresh --seed
```

![Migrate and Seed](https://raw.githubusercontent.com/codeadamca/laravel-blade-cms-journal/main/_readme/screenshot-migrate-seed.png)

If you received no errors, there will be tables with data in your database. OPen up phpMyAdmin to check!

![Entries Table](https://raw.githubusercontent.com/codeadamca/laravel-blade-cms-journal/main/_readme/screenshot-entries.png)
   
***

## Repository Resources

* [laravel-blade-cms](https://github.com/codeadamca/laravel-blade-cms)
* [Laravel](https://laravel.com/)

<a href="https://codeadam.ca">
<img src="https://codeadam.ca/images/code-block.png" width="100">
</a>
