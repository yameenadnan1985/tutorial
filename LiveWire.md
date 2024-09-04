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
<input wire:model="name" type="text" id="name" name="name" />
<input wire:model="email" type="text" id="email" name="email" />
<input wire:model="password" type="text" id="password" name="password" />
```
