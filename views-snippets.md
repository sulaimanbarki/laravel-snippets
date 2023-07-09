## Views (Blade Files)

- [Parse laravel $varaiables in Blade files <script> tag](#parse-laravel-variables-in-blade-script-tag)

### Parse laravel $variables in Blade <script> tag

```php
    // get statistics for all districts group by district, in controller
    $patients_statistics = Patient::select('district_id')
        ->selectRaw('count(*) as total')
        ->groupBy('district_id')
        ->get();

    // then in the blade file, inside the <script> tag
    <script>
    var total = {!! json_encode($patients_statistics->pluck('total')) !!} ;
    var district_name = {!! json_encode($patients_statistics->pluck('district_name')) !!} ;
    </script>
```