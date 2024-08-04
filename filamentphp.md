**Create new resource**
```
php artisan make:filament-resource User;
It will create new file inside App\filament\UserResource and a directory UserResource
```
**To Add New input**
```
use Filament\Forms\Components\TextInput;
TextInput::make('name')
->required();
```

**Create button**
```
Action::make('import')
```

**Button with URL**
```
use App\filament\resources\EmailSettingResource;

Action::make('emailSettings')
->label(__('Email Settings'))
->url(EmailSettingResource::getUrl()),
```
**Restrict Access of Admin only**
```
public static function canAccess(): bool
{
        return auth()->user()->is_admin;
}
```
**Add button to head section of Page**<br>
// To add button to header section of page use getHeaderActions()
```
protected function getHeaderActions(): array
{
        return [
            Action::make('import')
                ->label(__('Import Data'))
                ->url(ImportExcel::getUrl()),
            Action::make('formSettings')
                ->label(__('Student Form Setting'))
                ->url(FormSettingResource::getUrl()),
        ];
}
```
**Modal forms**<br>
Confirmation Model
```
Use App\Models\Post;

Action::make('delete')
    ->action(fn (Post $record) => $record->delete())
    ->requiresConfirmation()
```
**Simple Model Form**
```
Use App\Models\Post;
use Filament\Forms\Components\InputText;

Action::make('delete')
    ->form([
        InputText::make('first_name'),
        InputText::make('last_name')
])
```
