## Eloquent Relationship

- [Relationship with 'with' method](#relationship-with-eloquent-with-method)


### Relationship with eloquent with method

Relationship with model with the 'with' eloquent method to get specific fields
```php
    return Appointment::query()
        ->with('client:id,first_name,last_name')
        ->latest()
        ->paginate();
```