**Laravel**

**Good Videos:**
```
https://www.youtube.com/watch?v=M_XM0XxdVS4&list=PL8p2I9GklV45jJzLsexf2_hNNafpCXw9k&index=6
https://www.youtube.com/watch?v=kiH88gENxZM&list=PLe30vg_FG4OSCTUv3XIkwH--cK2D7rfJJ&index=4
```

**Display Error**
```
APP_ENV=local	
# This will enable error view

APP_ENV=production 
# This will disable error view

Config/app.php	
'debug' => env(false),

dd($name);
```

**Important Artisan Commands**
```
php artisan serve

# To get php artisan command help
php artisan help make:controller

php artisan make:controller welcomeController –plain
php artisan make:model ModelName
php artisan make:migration
php artisan make:seeder
php artisan make:middleware MiddlewareName
# If you want to see list of routes
php artisan route:list
# Create symbolic link
php artisan storage:link	
```

**Install Specific Laravel Version**
```
# To check php and compatible version go here
https://laravel.com/docs/5.5#server-requirements

Installing specific version of laravel in specific directory using composer
composer create-project laravel/laravel:5.5 ./
// =5.5		=	Version number
./		=	Current directory
```

**Install Latest version of Laravel**
```
To install laravel in current directory
composer create-project laravel/laravel ./
```

**Connect to Database**
```
connect to db by entering credentials in .env and config/database.php
```

**Install Authentication Package**
```
# Before installing authentication package you need to install node js

composer create-project laravel/laravel:”7.*” ./
composer require laravel/ui:”2.*”
php artisan ui:auth
php artisan ui  bootstrap 
npm install
npm run dev
php artisan migrate
```

**Authentication package:**
```
@auth	=	Check if user is logged in or not
auth()->user()->update(array);	// To update authenticated user
```

**Migrations**
```
Create new table using migration
php artisan make:migration create_articles_table –create=”articles”
```

**Migration - Modify table before production**
```
Step 1: php artisan migrate:rollback
Step 2: Make change in migration files inside database/migrations/
Step 3: php artisan migrate
```

**Migration - Modify table after production**
```
Step 1: php artisan make:migration add_new_column_to_articles_table –table=”articles”
Step 2: Make change to migration files inside database/migrations/

Example: 
function up() {
	$table->string("body")->nullable();
}
function down() {
	$table->dropColumn("body");
}
Step 3: php artisan migrate
```

**Migration - Reset all table**
```
php artisan migrate:fresh // Drop all tables and recreate
or  
php artisan migrate:refresh // reset and rerun all migrations
This command will drop all the tables and recreate the tables.
```

**Migration bug**
```
php artisan migrate
In case of error:
Edit the database.php file in config folder.

'charset' => 'utf8mb4',
'collation' => 'utf8mb4_unicode_ci',

to

'charset' => 'utf8',
'collation' => 'utf8_unicode_ci',
```
**Seeder**
```
Step 1:
php artisan make:seeder TableNameTableSeeder
# Convention TableName, Table, Seeder. Example: ArticlesTableSeeder
Step 2:
# A new file created inside database/seeds
# open ArticlesTableSeeder.php in editor and in run method add insert statement in run method
# Example, note 2 arrays
public function run() {
	DB::table('articles')->insert([
	[
		'title' => 'page1',
		'body'	=> 'Article body'	
	]
	]);
}
Step 3:
# In run() method of DatabaseSeeder.php add this line
public function run () {
	$this->call([ArticlesTableSeeder::class]);
}

Step 4:
composer dump-autoload

Step 5:
php artisan db:seed
```


**Model - Conventional CURD**
```
insert query
DB::insert(‘insert into article (name, title) values (?, ?)’, [‘adnan’, ‘this is test’]);

select query
$users = DB::select(‘Select * from article’);
return $users;

update
$users = DB::update(‘update article set body = ? where id = 2’, [‘bbbbbbb’]);

Delete
DB::delete(‘delete from articles where id = 2’);
```

**Model - ORM (object relational mapping)**
```
Always create model name as singular and table name as plural
e.g table name users model name user

php artisan make:model Article

CRUD
Façade: Use façade approach to update user in which do not initialize user/we do not create object

Insert:
$data = [
	‘title’		=>	‘This is title’,
	‘body’		=>	‘This is body’,
	‘password’	=>	bcrypt(‘password’)
];
Article::create($data);

Select:
Article::all();
Article::all()->toArray();
Article::find(1);
Article::where(‘name’,’adnan’);

Order By:
Article::latest(‘published_at’)->get();
Article::sortBy(‘published_at’,’desc’)->get();

Update:
Article::where(‘id’, 3)->update([‘name’ => ‘Test’, ‘Age’ => 45] );

Delete:
Article::where(‘id’,3)->delete();

Insert: 
Create Object of Article Class, assign properties and use save method 
$article = new Article();
$article->title = ‘title’;
$article->body = ‘body’;
$article->save();
```
**Model - one to many**
```
# User has many articles 
# In User model
public function articles (): HasMany {
	return $this->hasMany(Article::class, 'user_id', 'user_id');
}

# One article belong to one user
# In Arrticle model write this
public function user () {
	$this->belongsTo(User::class, 'user_id', 'user_id');
}
```
**Model - Many to Many**
```
# One category belong to many posts, one post belong to many category

Category.php model
public function posts (): BelongsToMany {
	$this->belongstoMany(Post::Class, 'category_id', 'category_id');
}

Post.php model 
public function categories (): BelongsToMany {
	$this->belongstoMany(Category::Class, 'post_id', 'post_id');
}
```
**HasManyThrough**<br>
1st Parameter: RelatedTO (Lesson::Class)<br>
2nd Parameter: Through (StudentLessonProgress::Class)<br>
3rd Parameter: Foreignkey of "Student" in "StudentLessonProgress" i,e "student_id"<br>
4th Parameter: Foreignkey of "StudentLessonProgress" in "Lesson" i,e "lesson_id"<br>
5th Parameter: Localkey Of Student i,e "student_id"<br>
6th Parameter: Localkey Of StudentLessonProgress i,e "lesson_id"
```
// This code is written in Student Model
public function lessons(): HasManyThrough
{
	return $this->hasManyThrough(Lesson::class, StudentLessonProgress::class, 'student_id', 'lesson_id', 'student_id', 'lesson_id');
}
```
**Disable timestamps**
```
public $timestamps = false;
```
**Disabling autoincrement**
```
public $incrementing = false;
```
**Get Single Value**
```
$group_name = Group::query()->where('group_id', '=', $groupId)->value('group_name');
```
**protected $with**<br>
protected $with property means that whenever you retrieve instances of the model, the specified relationships will automatically be loaded
```
protected $with = ['studentCC', 'studentRecurringPayments'];
```
**protected $appends**
```
protected $appends = [
        'first_name',
	'address'
];
public function getFirstNameAttribute(): string
{
        return (string) $this->user->address;
}
public function getAddressAttribute(): string
{
        return (string) $this->user->first_name;
}
```
**Collection with Example**<br>
A collection is an advanced, flexible wrapper around arrays of data<br>
When you retrieve data from the database using Eloquent, Laravel automatically wraps the result in a collection:<br>
In example below $users is collection
```
Common collection methods
->all()
->map()
->each()
->pluck() // Retrieves all values for a given key from the collection.
->filter()
->contains()
->first()
->sort()
->groupBy()
->count()

$users = DB::table('users')->get();
```
**Modify timestamp columns**
```
const CREATED_AT = 'entry_time';
const UPDATED_AT = 'update_time';
```
**protected $casts**<br>
When you define a cast on a model attribute, Laravel will automatically cast the attribute to the specified type when you access it.
```
protected $casts = [
        'is_admin' => 'boolean',   // Casts 'is_admin' to a boolean
        'created_at' => 'datetime', // Casts 'created_at' to a Carbon instance (date/time)
        'age' => 'integer',        // Casts 'age' to an integer
        'balance' => 'float',      // Casts 'balance' to a float
];
```
**where/whereRelation**<br>
whereRelation('TableName', 'ColumnName', 'ComparisonOperator', 'Value')
```
$studentLessonProgresses = StudentLessonProgress::query()
->where('survey_flag', '!=', true)
->whereRelation('schedule','product_type', '!=', ScheduleProductType::BLOCK->value)
->get();
```
**Model $table**
```
By default, Laravel expects the table name to be the plural form of the model name (e.g., for a model User, it expects a table named users). If your table name does not match this convention, you need to explicitly define it using the $table property.
```
**Model $fillable**
```
In model we add this
protected $fillable = [
	‘title’,
	‘body’,
];

And in controller if we do like 
$data = [
	‘title’		=>	‘This is title’,
	‘body’		=>	‘This is body’,
	‘password’	=>	‘password’
];
Article::create($data);
It will insert only title and body and will ignore password

If I want all fields to be fillable without mass assignment then I can do
protected $guarded = [];
```


**Model $guarded**
```
$guarded = ['name', 'email'];
# It means we want to ignore only name & email we don't want to insert values of name & email colmn
```


**Model $hidden**
```
If you want to remove fields like password in Article::all(); then in model add this
protected $hidden [
	‘password’,
	‘created_at’
]
```


**Model Accessor/Mutator**
```
# Mutator:
# Inside model create a function like below
# Convention set, DBFieldName, Attribute ($DBFieldName) {
	$this->attributes['dbfieldname'] = bcrypt($dbfieldname);
}
function setPasswordAttribute ($password) {	
	$this->attributes[‘password’] = bcrypt($password);
}

So now if you will do like this in controller it will encrypt the password and insert in DB
$data = [
	‘title’		=>	‘This is title’,
	‘body’		=>	‘This is body’,
	‘password’	=>	 ‘password’
];
Article::create($data);



Accessor:
Inside model create a function like below
function getTitleAttribute ($title) {	
	return ‘My title is: ’ . ucfirst($title);
}

In controller
$article = Article::all();
# it will return "My title is: Yameen Adnan"
return $article;
```


**Modal - $dates**
```
# To convert any date field to be istance of Carbon do this
protected $dates [
'published_at',
'date_of_birth'
];
```


**Views**
```
resources\views
In controller you can use 
return view(‘welcome’);	
// Which is equal to welcome.blade.php
{{  $name }}			
// Will display value of variable

{{ !!$name }}			
// This will display $name + will run html characters on page

Example: $name = ‘<span style=”color:red;”>Yameen Adnan</span>’

{{  $name }} = <span style=”color:red;”>Yameen Adnan</span>
{{  !!$name }} = Yameen Adnan
<a href=”{{ url(‘/article’,$article->id) }}”>Yameen Adnan</span>

Blade Engine
@extends(“layout.app”)		
// This is a bit like include or require
template.blade.php or layout.blade.php or master.blade.php
<html>
	<head>
		<title></title>
	</head>
	<body>
		<div class=”container”>
			@yield(‘content’);
		</div>
		@yield(‘footer’);
	</body>
</html>

// To add csrf to page add only @csrf
@csrf

child.blade.php
@extends(‘template’);

@section(‘content’)
<h1>Content section</a>
This test content section. This is CNN test section
@stop

@section(‘footer’)
<h1>This is footer section</a>
This test content section. This is CNN test section
@stop

@if ()
@endif

@if ()
@else
@endif

@unless = if !
<ul>
@foreach ( $persons as $person )
	<li>{{ $person }}</li>
@endforeach
</ul>

and it will show like My name is: Adnan

# Include view or Subview
@include(‘layout.app’)	
# it will look for file inside views/layout/app.blade.php
```


**Controllers**
```
app\Http\Controllers
php artisan make:controller welcomeController --plain;
$data = [];
$data[‘name’] = ‘Adnan’;

#Passing data to view
return view (‘welcome’,$data);

# Redirect to specific page
return redirect(‘articles’);
```


**Form validation**
```
$validation_rules = [
‘name’	=>	‘required|max:255’,	
‘email’	=>	‘required|unique:manage_users’,
‘phone’	=>	‘required|number|regex:/[0-9]{11}/’,
];
max:255 is use to make sure that value entered in input box does not exceed to allowable length of column.

$request->validate($validation_rules);

If validation fails it returns error in $errors object. 
Note: its $errors not $error.
Validation rules apply in sequence it is given 
$errors->all() will return an array containing all errors


Custom error messages
$validation_rules = [
‘title’ => ‘required|max:255’
];

$messages = [
‘title.required’ => ‘My dear must add title’,
‘title.max’ => ‘My dear do not exceed 255 characters’
];
$validatr = Validator::make ($request->all(), $validation_rules, $messages);
If ($validatr->fails())
return redirect()->back();
// rest of all code.
```


**Middleware**
```
Step 1:
php artisan make:middleware AuthUser
# This will create a new file inside app\Http\Middleware\AuthUser

Step 2:
# Add rules in middleware
# Important here is $request object
public function handle(Request $request, Closure $next) {

}
if ( $request->url(‘/store’) ) {
	// Add validation rules for store
} elseif ($request->url(‘update’)) {
	// Add validation rules for store
}

Step 3:  
# Add entry in \App\Http\kernel.php like below be careful of path when adding in kernel.php and controller.php
# This file contains 2 types of variables
# This applies to all routes
protected $middleware = [];

# This applies to specific routes
protected $routeMiddleware = [];

protected $routeMiddleware = [
'authStore' => \App\Http\Middleware\authStore::class,
];

Step 4:
# Create constructor in controller for which you created middleware e.g
class userController extends Controller
{
    public function __construct()
    {
        $this->middleware('authStore');
    }
}
```


**Routes**
```
routes/web.php file contains routing information
Routes::get(‘/’,’WelcomeController@index’);

# Dynamic route parameter
@ article/{id}/edit
So it can be 
article/1/edit
article/2/edit
article/3/edit and so on

function edit ($id) {
	echo ‘ID of article to edit is: ‘ . $id
}

```


**Scheduler in Laravel**
```
Step 1:
php artisan make:command TestCron --command=test:cron

Step 2:
Go insde app/console/commands/ and open TestCron.php
Add your function value inside handle ()
public function handle () {
	// write my function
}


Step 3:
Open app/console/kernel.php and add your function insdie $commands array
Example:
protected $commands = [
	Commands\TestCron::class,
];
and modify schedule function
Example:
protected function schedule (Schedule $schedule) {
	$schedule->command('test:cron')->hourly();
	// dalyAt('13:00'); etc
}

Step 4:
php artisan schedule:run
```



**Upload**
```
$request->file(‘myfile’);

Check if someone submitted the form after selecting the file.
$request->hasFile(‘myfile’);

To save file
$request->file(‘myfile’)->store(‘path’,’public’);

// We want to save file with our options
$request->file(‘myfile’)->storeAs(‘path’, ‘fileName’,’public’);

Get file name of client
$request->file(‘myfile’)->getClientOriginalName();

Access uploaded images:
// To show the image inside storage directory I need to create symbolic link
php artisan storage:link

// and it will create a link between /storage/app/public and /public. And if you want to access the image you can access it like asset(‘storage/images/’)
and it will create a link between /storage/app/public and /public. And if you want to access the image you can access it like asset(‘storage/images/’)

Deleted uploaded images:
Storage::delete(‘public/images/old-image.png’)

Open filesysystem inside config and see disks >> public

redirect
After form submission redirect back to form page
return redirect()->back();
```


**session**
```
After session()->put(‘message’, ‘This is test’);
If ( session()->has(‘message’) )
session()->get(‘message’)
```


**Encrypt password**
```
To encrypt password:
$data = [
'title'		=>	'First title',
'body'		=>	'First body',
'password'	=>	bcrypt(‘mypassword’),
];
Article::create($data);
```


**Datetime**
```
carbon (library):
Carbon is a laravel library that comes up with laravel install
use Carbon\Carbon;


$now = Carbon::now();
$now->format('Y-m-d H:i:s');
$now->addDays(10);
$now->addMonths(2);
$now->addYears(1);
```


**Localization**
```
Step1: 
# In view add like {{ __(‘profile.welcome’) }}	
# Here profile is the name of directory and fname is array key

Step2: 
# Create folder/file inside resources lang like
en/profile.php 
hi/profile.php
# Here profile is used in __(‘profile.welcome’)

Step3: 
en/profile.php contains
return [
‘welcome’	=>	“Welcome to My City”
];

hi/profile.php contains
return [
‘welcome’	=>	“कृपया प्रतीक्षा करें,”
];

Step4:
To set default
config/app.php >> locale and set ‘en’ or ‘hi’

To set dynamic
routes/web.php 
route::get(‘/profile/{lang}’,’controller@method’);

Step 5:
public function method($lang) {
	App::setlocal($lang);
}
```


**Install 3rd party packages**
```
composer require Package Name
Example:
composer require laravel/ui
```


**github**
```
When you have to commit changes to github ignore these
/vendor
.env
```


**tinker**
```
php artisan tinker
$article = new App\Article;
$article->title = ‘test’;
$article->title = ‘Another test’;
$article_array = $article->toArray();
$article->save();
```


**namespace**
```
Why use
If we add two classes with same name…it will give fatal error
To avoid this we use name space
```


**Any language basics for learning getting job**
```
Any language/framework: 
Basic (loop, ifelse, string, datetime)
Crud
Fileupload
Read Excel
Write PDF
Localization
Regular expressions
```

**If you add appenders then you must have to add getNameAttribute() function**

**Subqueries**
```
Subquery in select::
$orders = DB::table('orders')
    ->select('orders.*', DB::raw('(SELECT SUM(quantity) FROM order_items WHERE order_items.order_id = orders.id) as total_quantity'))
    ->get();


Subquery in where::
$orders = DB::table('orders')
    ->whereIn('id', function($query) {
        $query->select('order_id')
              ->from('order_items')
              ->groupBy('order_id')
              ->havingRaw('SUM(quantity) > ?', [10]);
    })
    ->get();


Subquery in From::
$orders = DB::table(DB::raw('(SELECT order_id, SUM(quantity) as total_quantity FROM order_items GROUP BY order_id) as sub'))
    ->where('total_quantity', '>', 10)
    ->get();

Subquery in Join::
$orders = DB::table('orders')
    ->leftJoin(DB::raw('(SELECT order_id, SUM(quantity) as total_quantity FROM order_items GROUP BY order_id) as oi'), 'orders.id', '=', 'oi.order_id')
    ->select('orders.*', 'oi.total_quantity')
    ->get();
```
