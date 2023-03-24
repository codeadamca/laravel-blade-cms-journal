# Journal Module for Laravel CMS

This is a basic journal module basaed on the Laravel CMS avalable in my [laravel-blade-cms](https://github.com/codeadamca/laravel-blade-cms) repo.

## Migrations

1. Using the Terminal, change the working directory to your project directory. I am using a Mac and my project folder was on my desktop:

    ``` sh
    cd ~
    cd Desktop
    cd laravel-blade-cms
    ```

2. Using the Laravel Artisan tool, create a new migration file:

    ```sh
    php artisan make:migration create_entries_table
    ```
    
    You will now have a new migration file named `<YEAR>_<MONTH>_<DAY>_<SECONDS>_create_entries_table.php`.
    
    
    > **Note** 
    > Laravel uses a database naming convention named [Eloquent](https://laravel.com/docs/10.x/eloquent). Eloquent states that tables names are lowercase and plural.  

3. In the new migration file, change the schema to:

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

We need a new model to define the `entries` table relationships, etc... The model scaffolding that Artisan provides is sufficient, no changes needed.

1. Create a new `Entry` model: 

    ```sh
    php srtisan make:model Endry
    ```
    
## Factory

We need an `Entry` factory to give Laravel instrcutions on how to populate the factory table. 

1. Creat a new factory:

    ```sh
    php artisan make:factory EntryFactory
    ```
    
2. You will now have a filed named `EntryFactory.php` in the `/database/factories` folder. Open thhis faile and change the definiation method retrn value to:

    ```php
    return [
        'title' => $this->faker->sentence,
        'content' => $this->faker->paragraph,
        'learned_at' => $this->faker->dateTimeThisMonth,
    ];
    ```
    
## Seeding




    
***

## Repository Resources

* [laravel-blade-cms](https://github.com/codeadamca/laravel-blade-cms)
* [Laravel](https://laravel.com/)

<a href="https://codeadam.ca">
<img src="https://codeadam.ca/images/code-block.png" width="100">
</a>
