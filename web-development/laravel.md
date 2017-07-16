```
Route::get('/', 'Welcome@index')->name('home.index');
```

```
//Will call the index() method on Welcome Controller
Route::get('about', function() {
return view('about');
});
```

```
// Return the about page on views folder
Route::post('verify', function(Request $request) {
return $request->input('username');
});
```

```
//will accept the input named username
php artisanmake:controllerWelcome
```

```
//command that will automatically create the Welcome controller
php artisanmake:controllerMySampleResourceController --resource
```

```
Example 3-23. Binding basic form actions
// routes/web.php
Route::get('tasks/create', 'TasksController@create');
Route::post('tasks', 'TasksController@store');
```

```
Example 3-24. Common form input controller method
// TasksController.php
...
public function store()
{
$task = new Task;
$task->title = Input::get('title');
$task->description = Input::get('description');
$task->save();
return redirect('tasks');
}
```

```
Example 3-25. Controller method injection viatypehinting
// TasksController.php
...
public function store(\Illuminate\Http\Request $request)
{
$task = new Task;
$task->title = $request->input('title');
$task->description = $request->input('description');
$task->save();
return redirect('tasks');
}
```



