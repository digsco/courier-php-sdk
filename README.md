# Courier SDK

Courier PHP SDK supporting:
* Send API
* Messages API
* Profiles API
* Preferences API

## Official Courier API docs

For a full description of request and response payloads and properties, please see the [official Courier API docs](https://docs.trycourier.com/reference).

## Requirements

* PHP 7.2+
* ext-curl
* ext-json

## Installation

```bash
composer require digs/courier-sdk-php
````

## Configuration

Instantiate the Courier client class with your authorization and (optional) username. Providing just a authorization token will generate a "Bearer" authorization header, while providing a username will generate a "Basic" (base64-encoded) authorization header

```php
$client = new Courier("authorization-token", "username");
```

### Options

Many methods allow the passing of optional data to the Courier endoint. This data should be an associative array of key/value pairs. The exact options supported are dependent on the endpoint being called. Please refer to the official Courier documentation for more information.

```php
$profile = [
	"firstname" => "Johnny",
	"lastname" => "Appleseed",
	"email" => "johnny.appleseed@mail.com"
];
```

## Methods

For a full description of request and response payloads and properties, please see the [official Courier API docs](https://docs.trycourier.com/reference).

### Send API

* ```sendNotification(string $event, string $recipient, array $profile = [], array $data = [], array $preferences = [], array $overrides = []): object``` [[?]](https://docs.trycourier.com/reference#post-send)

### Messages API

* ```getMessage(string $message_id): object``` [[?]](https://docs.trycourier.com/reference#post-statusrequest_id)

### Profiles API

* ```getProfile(string $recipient_id): object``` [[?]](https://docs.trycourier.com/reference#get-preferencesrecipient_id)
* ```upsertProfile(string $recipient_id, array $profile_attributes): object``` [[?]](https://docs.trycourier.com/reference#post-profilesid)
* ```replaceProfile(string $recipient_id, array $profile_attributes): object``` [[?]](https://docs.trycourier.com/reference#put-profilesid)
* ```patchProfile(string $recipient_id, array $patch): object``` [[?]](https://docs.trycourier.com/reference#patch-profilesid)

### Preferences API

* ```getPreferences(string $recipient_id, string $preferred_channel): object``` [[?]](https://docs.trycourier.com/reference#get-preferencesrecipient_id)
* ```updatePreferences(string $recipient_id, string $preferred_channel): object``` [[?]](https://docs.trycourier.com/reference#put-preferencesrecipient_id)

## Errors

All unsuccessfull (non 2xx) responses will throw a ```CourierRequestException```. The full response object is available via the ```getResponse()``` method.
