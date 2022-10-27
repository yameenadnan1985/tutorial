**Basics to learn any language any framework**
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

https://www.youtube.com/watch?v=M_XM0XxdVS4&list=PL8p2I9GklV45jJzLsexf2_hNNafpCXw9k&index=6

Good Videos:
https://www.youtube.com/watch?v=kiH88gENxZM&list=PLe30vg_FG4OSCTUv3XIkwH--cK2D7rfJJ&index=4


When you have to commit changes to github ignore these
/vendor
.env
Install Laravel
Installing specific version of laravel in specific directory using composer
composer create-project laravel/laravel:7.* ./
// =7.*		=	Version number
./		=	Current directory

To install laravel in current directory
composer create-project laravel/laravel ./

Artisan Commands
To get php artisan command help
php artisan serve
php artisan help make:controller
php artisan make:controller welcomeController –plain
php artisan make:model ModelName
php artisan make:migration
If you want to see list of routes
php artisan route:list
php artisan storage:link	// Create symbolic link
	


Install Authentication Package

Before installing authentication package you need to install node js

composer create-project laravel/laravel:”7.*” ./
composer require laravel/ui:”2.*”
php artisan ui:auth
php artisan ui  bootstrap 
npm install
npm run dev
php artisan migrate

Authentication package details:
@auth	=	Check if user is logged in or not
auth()->user()->update(array);	// To update authenticated user


		Connect to Database
connect to db by entering credentials in .env and config/database.php



Migrations
Migrations are version control of your database

Create new table using migration
php artisan make:migration create_articles_table –create=”articles”

Modify table using migration
php artisan make:migration add_new_column_to_articles_table –table=”articles”

Delete all tables to add new column
If you want to add new column to table and not care about data then run command below
php artisan migrate:fresh // Drop all tables and recreate
or  
php artisan migrate:refresh // reset and rerun all migrations
This command will drop all the tables and recreate the tables.

migration bugs
php artisan migrate
If receive error do this
Edit the database.php file in config folder.

'charset' => 'utf8mb4',
'collation' => 'utf8mb4_unicode_ci',

to

'charset' => 'utf8',
'collation' => 'utf8_unicode_ci',




Display Error

Much cleaner way to replace var_dump (To figure out reason of error)
dd($name);   // die and dump
At the top dd($name) contains which file was effected so that we can diagnose the class
Enable/Disable Error Display in Laravel:
Rename env.example to env if already have env do this
APP_ENV=local	
// This will enable error view
APP_ENV=production 
// This will disable error view
Config/app.php	
'debug' => env(false),



Routes
routes/web.php file contains routing information
Routes::get(‘/’,’WelcomeController@index’);

Controllers
Controllers Resides inside app\Http\Controllers
php artisan make:controller welcomeController --plain;
$data = [];
$data[‘name’] = ‘Adnan’;
Passing data to view
return view (‘welcome’,$data);

Views
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

// To add csrf to page do this
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







Model
Eloquent/Model/Object Relation Model:

Conventional CURD
insert query
DB::insert(‘insert into article (name, title) values (?, ?)’, [‘adnan’, ‘this is test’]);

select query
$users = DB::select(‘Select * from article’);

return $users;

update
$users = DB::update(‘update article set body = ? where id = 2’, [‘bbbbbbb’]);

Delete
DB::delete(‘delete from articles where id = 2’);

ORM (object relational mapping)
Always create model name as singular and table name as plural
e.g table name users model name user

Make a model
php artisan make:model Article

Laravel Crud using ORM:

Insert: 
Create Object of Article Class, assign properties and use save method 
$article = new Article();
$article->title = ‘title’;
$article->body = ‘body’;
$article->save();

Another short way to insert user
$data = [
	‘title’		=>	‘This is title’,
	‘body’		=>	‘This is body’,
	‘password’	=>	bcrypt(‘password’)
];
Article::create($data);


Mass assignment:
In model we add this
protected $fillable = [
	‘title’,
	‘body’,
];

And in controller if we do like 

$data = [
	‘title’			=>	‘This is title’,
	‘body’		=>	‘This is body’,
	‘password’	=>	‘password’
];
Article::create($data);
It will insert only title and body and will ignore password

If I want all fields to be fillable without mass assignment then I can do

protected guarded = [];

Update:
Façade: Use façade approach to update user in which do not initialize user/we do not create object
Article::where(‘id’, 3)->update([‘name’ => ‘Test’, ‘Age’ => 45] );
Article

To encrypt password use 
$article->password = bcrypt(‘mypassword’);

Select:
NO NEED to CREATE Object of Article Class instead use Façade, here is how
Façade: You don’t have to initialize / You don’t have to create object
$article = Article::all();
If you want to remove fields like password in Article::all(); then in model add this

protected $hidden [
	‘password’,
	‘created_at’
]

$article->delete()->where(‘id’, 2);

Delete:
Façade: You don’t have to initialize / You don’t have to create object
1st get user then delete
Article::where(‘id’,3)->delete();

Accessor and mutator:

Mutator:

Inside model create a function like below
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
	
	return ‘My name is: ’ . ucfirst($title);

}

In controller

$article = App\Article::all();

return $article;

and it will show like My name is: Adnan

tinker

php artisan tinker

$article = new App\Article;

$article->title = ‘test’;

$article->title = ‘Another test’;

$article_array = $article->toArray();

$article->save();


App\Article::all()->toArray();

App\Article::find(1);
$name = App\Article::where(‘name’,’adnan’);

Order By:
App\Article::latest(‘published_at’)->get();

Or

App\Article::sortBy(‘published_at’,’desc’)->get();



Install 3rd party packages

composer require Package Name

Example:
composer require laravel/ui

When we will add this package and go to command prompt and do like







Datetime
carbon (library):
Carbon is a laravel library that comes up with laravel install

$now = Carbon\Carbon::now();

Redirect to specific page:

return redirect(‘articles’);


Why use namespace:
If we add two classes with same name…it will give fatal error

To avoid this we use name space



Form Validation
// Validation rules
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
$rules = [
‘title’ => ‘required|max:255’
];

$messages = [
‘title.required’ => ‘My custom error message’,
‘title.max’ => ‘My custom max error message’
];
$validatr = Validator::make ($request->all(), $rules, $messages);
If ($validatr->fails())
return redirect()->back();
// rest of all code.
Middleware

Step 1
php artisan make:middleware CustomMiddleWare

Important here is $request object

Step 2   // Add rules in middleware
if ( $request->url(‘/store’) ) {
	// Add validation rules for store
} elseif ($request->url(‘update’)) {
	// Add validation rules for store
}

Step 3  // Add entry in \App\Http\kernel.php like below be careful of path when adding in kernel.php and controller.php	

'FormValidation' => \App\Http\Middleware\FormValidationRules::class,

Step 4 // Create constructor in controller for which you created middleware e.g

class userController extends Controller
{
    public function __construct()
    {
        $this->middleware('FormValidation',['only' => 'store']);
    }
}



Image Handling

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

Session
After session()->put(‘message’, ‘This is test’);
If ( session()->has(‘message’) )
session()->get(‘message’)


Include view or Subview
@include(‘layout.app’)	
// it will look for file inside views/layout/app.blade.php






Dynamic route parameter
@ article/{id}/edit
So it can be 
article/1/edit
article/2/edit
article/3/edit and so on

function edit ($id) {
	echo ‘ID of article to edit is: ‘ . $id
}



Localization
Step1: In view add like {{ __(‘profile.welcome’) }}	
// Here profile is the name of directory and fname is array key

Step2: Create folder/file in inside resources lang like
en/profile.php // Here profile is used in __(‘profile.welcome’)
hi/profile.php

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

Step 4:
public function method($lang) {
	App::setlocal($lang);
}
