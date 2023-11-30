```php
Route::get('/cache-clear', function() {
    Artisan::call('config:cache');
    Artisan::call('cache:clear');
    Artisan::call('view:clear');
    Artisan::call('queue:restart');
    return "Cache clear";
});

```
