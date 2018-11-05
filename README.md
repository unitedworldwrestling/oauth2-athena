# UWW Athena Provider for OAuth 2.0 Client

This package provides Athena OAuth 2.0 support for the PHP League's [OAuth 2.0 Client](https://github.com/thephpleague/oauth2-client).

## Installation

To install, use composer:

```
composer require unitedworldwrestling/oauth2-athena
```

## Usage

Usage is the same as The League's OAuth client, using `\Unitedworldwrestling\OAuth2\Client\Provider\Athena` as the provider.

### Client Credentials Flow

```php
$provider = new Unitedworldwrestling\OAuth2\Client\Provider\Athena([
    'clientId'          => '{athena-client-id}',
    'clientSecret'      => '{athena-client-secret}',
    'redirectUri'       => 'https://example.com/callback-url',
    'host'              => 'https://api.instagram.com' // Optional, defaults to https://api.instagram.com
]);


// Try to get an access token (using the https://athena.uww.io/grants/api_key grant)
$token = $provider->getAccessToken('https://athena.uww.io/grants/api_key');

// Optional: Now you have a token you can look up a users profile data
try {

    // We got an access token, let's now get the user's details
    $user = $provider->getResourceOwner($token);

    // Use these details to create a new profile
    printf('Hello %s!', $user->getName());

} catch (Exception $e) {

    // Failed to get user details
    exit('Oh dear...');
}

// Use this to interact with an API on the users behalf
echo $token->getToken();
```