# Match expression

```php
$status = 'completed';
$result = match($status) {
	'completed' => 'Order is complete',
	'pending' => 'Order is pending',
	default => 'Unknown status',
};
echo $result; // Order is complete
```
