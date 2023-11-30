## How to create and migrate the seedor

```
php artisan make:seeder UsersTableSeeder
php artisan db:seed --class=UsersTableSeeder
```

## How to clear packages and project

```
composer dump-autoload
php artisan optimize:clear
```
