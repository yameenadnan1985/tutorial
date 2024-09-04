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
