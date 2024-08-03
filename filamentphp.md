**Create button**
``
Action::make('import')
``

**Button with URL**
``
use App\filament\resources\EmailSettingResource;

Action::make('emailSettings')
->label(__('Email Settings'))
->url(EmailSettingResource::getUrl()),
``
