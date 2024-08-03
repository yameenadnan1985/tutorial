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
**Add button to head section of Page**
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
