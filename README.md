# exponent-server-sdk-php
Server-side library for working with Expo push notifications using PHP

# Usage
- Require the package in your project
```bash
composer require kozhindev/exponent-server-sdk-php
```
- In a php file
```php
    require_once __DIR__.'/vendor/autoload.php';
    
    $channelName = 'news';
    $token = 'ExponentPushToken[unique]';
    
    $expo = new \ExponentPhpSDK\Expo();
    
    // Build the notification data
    $notification = ['body' => 'Hello World!'];
    
    // Notify a token (or several tokens) with a notification
    $expo->notify([$token], $notification);
 ```
Data can be added to notifications by providing it as a JSON object. For example:
```php
// Build the notification data
$notification = ['body' => 'Hello World!', 'data'=> json_encode(array('someData' => 'goes here'))];
```

# Additional security

If you set up enhanced security in your Expo Dashboard (as described [here](https://docs.expo.io/push-notifications/sending-notifications/#additional-security)), you will need to attach an authorization token to each push request:

```php
    // ...
    
    // Bootup an expo instance
    $expo = \ExponentPhpSDK\Expo::normalSetup();
    
    // Fetch your access token from where you stored it
    $accessToken = 'your_expo_access_token';
    
    // The access token will be attached to every push request you make hereafter
    $expo->setAccessToken($accessToken);
    
    // Notify an interest with a notification
    $expo->notify([$channelName], $notification);
 ```