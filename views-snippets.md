## Views (Blade Files)

- [Parse laravel $varaiables in Blade <script> tag](#parse-laravel-variables-in-blade-script-tag)

### Parse laravel $variables in Blade <script> tag

```php
    // get statistics for all districts group by district
    $patients_statistics = Patient::select('district_id')
        ->selectRaw('count(*) as total')
        ->groupBy('district_id')
        ->get();

    // then in the blade file
    var total = {!! json_encode($patients_statistics->pluck('total')) !!} ;
    var district_name = {!! json_encode($patients_statistics->pluck('district_name')) !!} ;
```