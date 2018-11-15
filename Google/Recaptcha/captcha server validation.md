# I. Create Repo From Existing Project
**Case :**  
I allready implement google recaptcha on frontend and need to validate on my server side
**Update Version:**  
version 1 - 15 Nov 2018

**Environment**  
- Frontend Environment : html + js
- Backend : laravel
- Programming Tool : VS code

**Docs**  
https://developers.google.com/recaptcha/intro

**Step By Step**  
1. Config recaptcha key & secret inside **.env** file
  
2. Require guzzle on laravel,  open terminal on vs code and run **composer require guzzlehttp/guzzle**
  
3. Make new traits to handle recaptcha validation.  Ie : recaptchaTrait.php
```
<?php
namespace App\Http\Traits;

use GuzzleHttp\Client;

trait recaptchaTrait {
    public static function validateCaptcha($token = null) {
        $client = new Client([
            'base_uri' => 'https://google.com/recaptcha/api/'
        ]);

        $response = $client->post('siteverify', [
            'query' => [
                'secret' => env('GOOGLE_RECAPTCHA_SECRET'),
                'response' => $token,
                'verify' => false
            ]
        ]);

        return json_decode($response->getBody())->success;
    }
}
```

4.  Use trait on controller 
```
use App\Http\Traits\recaptchaTrait;

class frontendController extends Controller {
    use recaptchaTrait;

    public function validateCaptcha(Request $request){
        $result = recaptchaTrait::validateCaptcha("your request captcha token");
        if(!$result){
            // on validate error
            // your code
        }

        // on validate success
        // your code
    }
}
```

5.  Done

  
**Caveats**  
On windows 7, performing API Call would return an error : GuzzleHttp Exception cURL error 60 or 70. If you facing this, here is the solution.
1. Download certificate from link https://curl.haxx.se/ca/cacert.pem
2. Find the directory of php.ini. You can obtain the path by using the following script on your controller, and your path would be on **Loaded Configuration File** section
```
dd(phpinfo());
```
3. Copy your certificate inside the directory
4. Open your php.ini,  and add the following code
```
curl.cainfo="your directory path"

example
curl.cainfo="C:\tools\php72\cacert.pem"
```
5. save and restart your php service, or your pc