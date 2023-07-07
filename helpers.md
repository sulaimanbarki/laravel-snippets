## Helpers

- [Most useful date helper method now()](#laravel-now-helper-function-with-most-useful-usage)
- [Laravel helper request() method also returns collection](#laravel-helper-request-method-also-returns-collection)
- [Laravel collect() method](#laravel-collect-method)

### Laravel now() helper function with most useful usage

```php
    // get current date and time
    $now = now();
    // get current date
    $now = now()->toDateString();
    // get current time
    $now = now()->toTimeString();
    // get current date and time in a specific format
    $now = now()->format('Y-m-d H:i:s');


    $totalUsersCount = User::query()
        ->when(request('date_range') === 'today', function ($query) {
            $query->whereBetween('created_at', [now()->today(), now()]);
        })
        ->when(request('date_range') === '30_days', function ($query) {
            $query->whereBetween('created_at', [now()->subDays(30), now()]);
        })
        ->when(request('date_range') === '60_days', function ($query) {
            $query->whereBetween('created_at', [now()->subDays(60), now()]);
        })
        ->when(request('date_range') === '360_days', function ($query) {
            $query->whereBetween('created_at', [now()->subDays(360), now()]);
        })
        ->when(request('date_range') === 'month_to_date', function ($query) {
            $query->whereBetween('created_at', [now()->firstOfMonth(), now()]);
        })
        ->when(request('date_range') === 'year_to_date', function ($query) {
            $query->whereBetween('created_at', [now()->firstOfYear(), now()]);
        })
        ->count();
```

### Laravel helper request() method also returns collection

```php
    // normally we use Request $request in controller method to validate and get the request data
    $request->validate([
        'name' => 'required',
        'email' => 'required|unique:users,email',
        'password' => 'required|min:8',
    ]);
    
    // we can also use request() helper method to validate and get the request data
    request()->validate([
        'name' => 'required',
        'email' => 'required|unique:users,email',
        'password' => 'required|min:8',
    ]);
```

### Laravel collect() method

```php
    // collect() method is used to convert array to collection
    $array = [1, 2, 3, 4, 5];
    $collection = collect($array);
    // now we can use collection methods on $collection variable
    $collection->sum();
    $collection->avg();
    $collection->max();
    $collection->min();
    $collection->count();
    $collection->first();
    $collection->last();
    $collection->where('id', 1);
    $collection->where('id', 1)->first();
    $collection->where('id', 1)->last();
    $collection->where('id', 1)->count();
    $collection->where('id', 1)->sum();
    $collection->where('id', 1)->avg();
    $collection->where('id', 1)->max();
    $collection->where('id', 1)->min();


    // we can also pass array and get more structured data as a return

    $cases = AppointmentStatus::cases();

    return collect($cases)->map(function ($status) {
        return [
            'name' => $status->name,
            'value' => $status->value,
            'count' => Appointment::where('status', $status->value)->count(),
            'color' => AppointmentStatus::from($status->value)->color(),
        ];
    });
```