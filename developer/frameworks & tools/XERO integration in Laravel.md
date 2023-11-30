This integration has been implemented in `Ms-Metal-Work` project.

1. Create an account of [developer.xero.com](http://developer.xero.com/)

```
Email: koreex.jin@gmail.com
Password: koreex0xero
2FA-authenticator: google authenticator
Backup email: fanghuateng0621@gmail.com
```

1. Create a new app

```
App Name: ms-metal-works
Application URL: <https://ms.thinknew.nz>
Redirect URI: <https://ms.thinknew.nz/api/xero/redirect>
```

> NOTE: Application URL must be https.
> After creating an account, we can get Referral id called XTID

| Referral id     | Client id                        | Secret                                           |
| --------------- | -------------------------------- | ------------------------------------------------ |
| x30msmetalworks | 18C24A1DDFCE4939A67D67613B4572DE | 3jqaxQc_6oWvZ06UuZISK-iWLmiOq2DNyvzvOhpPftYOpNEh |

1. Install SDK

```bash
composer require ayles-software/xero-laravel
```

1. Publish vendor

```bash
php artisan vendor:publish --provider="AylesSoftware\\XeroLaravel\\ServiceProvider"
```

1. Config .env file

```
XERO_CLIENT_ID=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
XERO_CLIENT_SECRET=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
XERO_REDIRECT_URI=https://example.com/xero-callback
```

> NOTE: Reference - https://libraries.io/packagist/ayles-software%2Fxero-laravel

1. Run Xero migrations

```bash
php artisan migrate
```
