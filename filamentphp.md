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
Confirmation Model<br>
In model form there are few things important<br>
1- Action::make()<br>
2- ->fillForm(fn (Post $record): array => ['authorName' => $record->name])<br>
3- ->form([InputText::make('authorName')])<br>
4- ->action(fn(array $data, Post $record): void => $record->name = $data['authorName'])
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
**Get Modal Form data**<br>
The data from the Model Form is available in the $data array of the action() closure:
```
use App\Models\Post;
use App\Models\User;
use Filament\Forms\Components\InputText;
 
Action::make('updateName')
    ->form([
        InputText::make('name')
            ->required(),
    ])
    ->action(function (array $data, Post $record): void {
        $record->author()->name($data['name']);
        $record->save();
    })
```
**Fill Model Form with Existing Data**
```
use App\Models\Post;
use App\Models\User;
use Filament\Forms\Components\InputText;
use Filament\Forms\Form;
 
Action::make('updateAuthor')
    ->fillForm(fn (Post $record): array => [
        'authorName' => $record->author->name,
    ])
    ->form([
        InputText::make('authorName')
            ->label(__('Name'))
            ->required(),
    ])
```
