Yii2 users module.
==================
This module provide a users managing system for your yii2 application.

Installation
------------

The preferred way to install this extension is through [composer](http://getcomposer.org/download/).

Either run

```
php composer.phar require --prefer-dist vova07/yii2-users-module "*"
```

or add

```
"vova07/yii2-users-module": "*"
```

to the require section of your `composer.json` file.

Configuration
-------------

Add `yii2-users-module` to `module` section of each application config:

```php
'modules' => [
    'users' => [
        'class' => 'vova07\users\Module',
        'controllerNamespace' => 'vova07\users\controllers\backend', // For backend app. For frontend app just skip this param.
        'requireEmailConfirmation' => false, // By default is true. It mean that new user will need to confirm their email address.
        'robotEmail' => 'my@robot.email', // E-mail address from that will be sent all `users` emails.
        'robotName' => 'My Robot Name', // By default is `Yii::$app->name . ' robot'`.
        'activationWithin' => 86400, // The time before a sent activation token becomes invalid.
        'recoveryWithin' => 14400, // The time before a sent recovery token becomes invalid.
        'recordsPerPage' => 10, // Users pe page.
        'adminRoles' => ['superadmin', 'admin'], // User roles that can access backend module.
    ]
]
```

Add or edit `user` component section:

```php
'user' => [
    'class' => 'yii\web\User',
    'identityClass' => 'vova07\users\models\User',
    'loginUrl' => ['/users/guest/login']
]
```

Add or edit `authManager` component section:

```php
'authManager' => [
    'class' => 'yii\rbac\PhpManager',
    'defaultRoles' => [
        'user',
        'admin',
        'superadmin'
    ],
    'authFile' => '@vova07/rbac/data/rbac.php'
]
```

Run module migration:

```php
php yii migrate --migrationPath=@vova07/users/migrations
```

Usage
-----

Once the extension is installed, simply use it in your code by:

```php
Yii::$app->getModule('users');
```

By default will be created one `superadmin` user with login `admin` and password `admin12345`.

After installation you'll be able to access below links (relative to your site domain):
### Frontend: ###
- `/users/` - All users page
- `/users/admin/` - Admin page
- `/login/` - Log In page
- `/logout/` - Log Out page
- `/signup/` - Sign Up page
- `/recovery/` - Password recovery page
- `/resend/` - Resend email activation token
- `/activation/` - Accaunt activation page
- `/recovery-confirmation/` - Password reset page
- `/my/settings/email/` - Email change page
- `/my/settings/password/` - Password change page
- `/my/settings/update/` - Profile update page

### Banckend ###
You'll need to specify universal route `'<_m>/<_c>/<_a>' => '<_m>/<_c>/<_a>'` in your config file to access module actions.
- `/users/guest/login/` - Log In page
- `/users/user/logout/` - Log Out page
- `/users/default/index/` - All users page
- `/users/default/view/` - User page
- `/users/default/create/` - Create new user page
- `/users/default/update/` - Update user page
- `/users/default/delete/` - Delete one user
- `/users/default/batch-delete/` - Delete more users

Dependences
-----------
- [yii2-control-widget](https://github.com/vova07/yii2-control-widget)
- [yii2-rbac-module](https://github.com/vova07/yii2-rbac-module)
- [yii2-swiftmailer](https://github.com/yiisoft/yii2/tree/master/extensions/swiftmailer)
- [yii2](https://github.com/yiisoft/yii2)