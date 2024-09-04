**Make livewire component**
```
php artisan make:livewire componentName
It will generate 2 files
App/Livewire/ComponentName.php
resources/views/livewire/component-name.blade.php

Example:
php artisan make:livewire PrimeHoursWidget
It will generate 2 files
App/Livewire/PrimeHoursWidget.php
resources/views/livewire/prime-hours-widget.blade.php
```
**Display Livewire Component**
```
In the view add like this
@livewire('my-livewire-component');
or
<livewire:my-livewire-component />
```
**Click Event wire:click**
```
// View is located in recources/views/livewire/my-livewire-component.blade.php
<div>
<button wire:click="handleClick">
Click Me
</button>
</div>
App/Livewire/MyLivewireComponent.php

public function handleClick(): void
{
  dd('Test');
}
```
**Saving values from Livewire View into DB wire:model**
```
App/Livewire/MyLivewireComponent.php
public $name;
public $email;
public $password;

recources/views/livewire/my-livewire-component.blade.php
<form>
<input wire:model="name" type="text" id="name" name="name" />
<input wire:model="email" type="text" id="email" name="email" />
<input wire:model="password" type="text" id="password" name="password" />
<button wire:click.prevent="handleClick"></button>
</form>
```
**Form Validation**
```
App/Livewire/MyLivewireComponent.php
public $name;
public $email;
public $password;
public function handleClick(): void
{
  $this->validate(
    'name' => 'required|min:10',
    'email' => 'required|email',
    'password' => 'required'
  );
  User::create([
    'name' => $this->name,
    'email' => $this->email,
    'password' => $this->password
  ]);
}

recources/views/livewire/my-livewire-component.blade.php
<form>
<input wire:model="name" type="text" id="name" name="name" />
@error('name')
  {{$message}}
@enderror
<input wire:model="email" type="text" id="email" name="email" />
@error('email')
  {{$message}}
@enderror
<input wire:model="password" type="text" id="password" name="password" />
@error('password')
  {{$message}}
@enderror
<button wire:click.prevent="handleClick"></button>
</form>
```
**Common livewire Directives**
```
wire:model // for input
wire:click // for button
wire:click.prevent // for button
wire:submit.prevent // for form
wire:keydown // keypress
wire:keydown.enter // enter key press
wire:keydown.escape // escape key press
wire:loading
<button wire:click="save">
    Save
</button>
<span wire:loading>Saving...</span>
wire:poll // Like setTimeOut and ajax
<div wire:poll.5s="refreshData">
    <p>Latest Data: {{ $data }}</p>
</div>

wire:key
- Helps identify a DOM element uniquely within a loop, avoiding potential issues when re-rendering.

Example:
@foreach($items as $item)
    <div wire:key="item-{{ $item->id }}">
        {{ $item->name }}
    </div>
@endforeach
This ensures that each item in the loop is uniquely identified, preventing re-rendering issues.

wire:model.lazy = blur
Updates the component property only when the input loses focus, instead of on every keystroke.

Example:
<input type="text" wire:model.lazy="name">
The `name` property is updated only when the input field loses focus.

wire:model.debounce
Debounces updates to the component property, only sending updates after the user has stopped typing for a specified duration.

Example:
<input type="text" wire:model.debounce.500ms="name">
The `name` property is updated 500ms after the user stops typing.
```
