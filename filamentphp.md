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
**Type of Actions/Buttons**<br>
1- Page header actions (getHeaderActions)<br>
2- Table actions (Row Actions, Header Actions, Bulk Actions)<br>
3- Custom Livewire component actions<br>
**Page header actions**
```
protected function getHeaderActions(): array
{
        return [
            Action::make('import')
                ->label(__('Import Data'))
                ->url(ImportExcel::getUrl()),
        ];
}
```
**Table actions**<br>
1- Row actions<br>
2- Table header actions<br>
3- Bulk actions
```
public function table(Table $table): Table
{
    return $table
        ->actions([
	   Action::make('delete')
    		->requiresConfirmation()
    		->action(fn (Post $record) => $record->delete())
        ])
        ->headerActions([]),
        ->bulkActions([
	        ->requiresConfirmation()
                ->action(fn (Collection $records) => $records->each->delete())
        ])
}

```
**Button with URL**
```
use App\filament\resources\EmailSettingResource;

Action::make('emailSettings')
->label(__('Email Settings'))
->url(EmailSettingResource::getUrl()),
// To send data to page
->url(EmailSettingResource::getUrl($data)),
```
**Restrict Access of Admin only**
```
public static function canAccess(): bool
{
        return auth()->user()->is_admin;
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
**Get data from Modal**<br>
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
**Fill Model with Existing Data**<br>
To fill model with existing data use fillForm method
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
**Disabling All Form Fields**
```
Action::make('')
->form([])
->fillForm()
->disabledForm()
```
**Notifications**
```
use Filament\Notifications\Notification;

Notification::make()
    ->title('Saved successfully')
    ->success()
    ->body('Changes to the post have been saved.')
    ->send();

```
