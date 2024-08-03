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
***Restrict Access of Admin only***
```
public static function canAccess(): bool
{
        return auth()->user()->is_admin;
}
```
