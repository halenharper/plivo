# Laravel - plivo
[docs on web](http://lakshmajim.github.io/plivo/)
>##WHAT IT IS?

- This package is used to send sms to any mobile number.
- This uses [Plivo!](https://www.plivo.com/) API.
- It requires *AuthId* and *AuthToken*, they can be generated by registrting @at [Plivo](https://manage.plivo.com/dashboard/)
  - after registrion click on Dashboard ,there you will be able to see authid and authtoken. 
  - sample snapshot:
![Image of plivo dashboard](https://raw.githubusercontent.com/lakshmajim/images/master/plivo.png)




>##INSTALLATION

Download package form  https://github.com/lakshmajim/plivo . 
Place it in vendor directory of your project.
edit composer.json file
```bash
 "autoload": {
        "classmap": [
            "database"
        ],
        "psr-4": {
            "App\\": "app/",
            "lakshmajim\\plivo\\": "vendor/lakshmajim/plivo/src"   
        }
    },
```

Run this command from the Terminal:

```bash
    composer dumpautoload
    composer update
```

>##Laravel INTEGRATION

you need to add the service provider. Open `app/config/app.php`, and add a new item to the providers array.
```php
 lakshmajim\plivo\PlivoServiceProvider::class,
```
Then, add a Facade for more convenient usage. In `app/config/app.php` add the following line to the `aliases` array:
```php
'Plivo'     => lakshmajim\plivo\Facade\Plivo::class,
```

>##SENDING SMS

```php
<?php

Use Plivo;

Plivo::sendMessagePlivo($auth_id,$auth_token);
```

>##MISCELLANEOUS

```php
<?php

  Use Plivo;
  //setting source mobile number
  Plivo::setSourceMobile("918888888888");
  //setting destination mobile number
  Plivo::setDestinationMobile("919999999999");
  //setting text message
  Plivo::setMessagePlivo(" is!");
  //setting call back url
  Plivo::setCallBackUrl("http://localhost/");```
```


>##EXAMPLE CODE FOR Laravel

```php

<?php namespace App\Http\Controllers;

use Illuminate\Routing\Controller as BaseController;
use Plivo;

class Controller extends BaseController
{
       public function sendSMS()
    {
        $src  = Plivo::setSourceMobile("<SOURCE MOBILE NUMBER>");
        $dest = Plivo::setDestinationMobile("<RECEIVERS MOBILE NUMBER>");
        $txt  = Plivo::setMessagePlivo("<YOUR TEXT MESSAGE>");
        $url  = Plivo::setCallBackUrl("<YOUR_RETURN_BACK_URL>");
        $smsObject=Plivo::sendMessagePlivo('<YOUR_AUTH_ID>','<YOUR_AUTH_TOKEN>');
        echo "$smsObject";         //diaplay final message response
    }
}


```

>##LICENSE

[MIT License (MIT)](https://opensource.org/licenses/MIT)
