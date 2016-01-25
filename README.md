# oauth2-qq
QQ OAuth 2.0 support for the PHP League's OAuth 2.0 Client
##Useage
```php
session_start();
$provider = new \spoonwep\OAuth2\Client\Provider\qq([
	'clientId' => '{QQ APP ID}',
	'clientSecret' => '{QQ APP KEY}',
	'redirectUri' => 'http://example.com/callback-url',
]);
if (!isset($_GET['code'])) {
	$authUrl = $provider->getAuthorizationUrl();
	$_SESSION['oauth2state'] = $provider->getState();
	header('Location: '.$authUrl);
	exit;
} elseif (empty($_GET['state']) || ($_GET['state'] !== $_SESSION['oauth2state'])) {
	unset($_SESSION['oauth2state']);
	exit('Invalid state');
} else {
	$token = $provider->getAccessToken('authorization_code', [
		'code' => $_GET['code']
	]);
	$user = $provider->getResourceOwner($token);
	$user = $user->toArray();		
	print_r($user);
}
```
###License
The MIT License (MIT). Please see [License](https://github.com/spoonwep/oauth2-qq/blob/master/LICENSE.txt) File for more information.
