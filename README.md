# Yii2 Translate Panel

[Yii2](http://www.yiiframework.com) Translate Panel makes the translation of your application so simple.
It based on [i18n (internalization) module](https://github.com/zelenin/yii2-i18n-module) with greatly improved usability in mind (see screen shots below).

TODO Yii2 Translate Panel screens...


## Installation


### Composer

The preferred way to install this extension is through [Composer](http://getcomposer.org/).

Either run

```
php composer.phar require uran1980/yii2-translate-panel "dev-master"
```

or add

```
"uran1980/yii2-translate-panel": "dev-master"
```

to the require section of your ```composer.json```


## Usage

Configure "Yii2 Translate Panel" component in ```common/config/main.php```:

```php
$config = [
    ...
    'components' => [
        ...
        'i18n' => [
            'class'=> uran1980\yii\modules\i18n\components\I18N::className(),
            'languages' => ['en', 'de', 'fr', 'it', 'es', 'pt', 'ru'],
            'translations' => [
                '*' => [
                    'class'           => yii\i18n\DbMessageSource::className(),
                    'enableCaching'   => true,
                    'cachingDuration' => 60 * 60 * 2, // cache on 2 hourse
                ],
            ],
        ],
        ...
    ],
    ...
];
```

Configure "Yii2 Translate Panel" module in ```backend/config/main.php```:

```php
$config = [
    ...
    'modules' => [
        ...
        'i18n' => [
            'class' => uran1980\yii\modules\i18n\Module::className(),
            'controllerMap' => [
                'default' => uran1980\yii\modules\i18n\controllers\TranslationsController::className(),
            ],
            // example for set access to module (if required):
            'as access' => [
                'class' => yii\filters\AccessControl::className(),
                'rules' => [
                    'controllers'   => ['i18n/default'],
                    'actions'       => ['index', 'update'],
                    'allow'         => true,
                    'roles'         => ['admin'],
                ],
            ],
        ],
        ...
    ],
    ...
]
```

Run:

```
php yii migrate --migrationPath=@uran1980/yii/modules/i18n/migrations
```

Go to ```http://backend.yourdomain.com/translations``` for translating your messages


### PHP to DB import

If you have an old project with PHP-based i18n you may migrate to DbSource via console.

Run:

```
php yii i18n/import @common/messages
```

where ```@common/messages``` is path for app translations


### DB to PHP export

Run:

```
php yii i18n/export @uran1980/yii/modules/i18n/messages uran1980/modules/i18n
```

where ```@uran1980/yii/modules/i18n/messages``` is path for app translations and ```uran1980/modules/i18n``` is translations category in DB


### Using ```yii``` category with DB

Import translations from PHP files

```
php yii i18n/import @yii/messages
```

Configure "Yii2 Translate Panel" component:

```php
'i18n' => [
    'class'=> uran1980\yii\modules\i18n\components\i18n::className(),
    'languages' => ['en', 'de', 'fr', 'it', 'es', 'pt', 'ru'],
    'translations' => [
        'yii' => [
            'class'           => yii\i18n\DbMessageSource::className(),
            'enableCaching'   => true,
            'cachingDuration' => 60 * 60 * 2, // cache on 2 hourse
        ]
    ]
],
```


## Info

Component uses yii\i18n\MissingTranslationEvent for auto-add of missing translations to database

See [Yii2 i18n guide](https://github.com/yiisoft/yii2/blob/master/docs/guide/tutorial-i18n.md)


## Author

[Ivan Yakovlev](https://github.com/uran1980/), e-mail: [uran1980@gmail.com](mailto:uran1980@gmail.com)