## Elequent Methods

- [Laravel model 'through' method](#laravel-model-through-method)

### Laravel model 'through' method

Laravel model 'through' method is used mostly to restructure the data in a single statement

```php
    return Appointment::query()
            ->latest()
            ->paginate()
            // instead of using map(), transform() or other methods, we can use 'through' method to restructure the data
            ->through(fn ($appoinment) => [
                'id' => $appoinment->id,
                'start_time' => $appoinment->start_time->format('Y-m-d h:i A'),
                'end_time' => $appoinment->end_time->format('Y-m-d h:i A'),
                'status' => [
                    'name' => $appoinment->status->name,
                    'color' => $appoinment->status->color(),
                ],
            ]);
```