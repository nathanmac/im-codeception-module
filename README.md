Codeception Instant Messaging (IM) Module
=========================================

[![License](http://img.shields.io/packagist/l/nathanmac/im-codeception-module.svg)](https://github.com/nathanmac/im-codeception-module/blob/master/LICENSE.md)
[![Release](http://img.shields.io/github/release/nathanmac/im-codeception-module.svg)](https://github.com/nathanmac/im-codeception-module/releases)


This module will let you test messages that are sent during your Codeception
acceptance tests.

## Installation

Begin by installing this package through Composer. Edit your project's `composer.json` file to require `nathanmac/im-codeception-module`.

    {
        "require-dev": {
            "codeception/codeception": "*",
            "nathanmac/im-codeception-module": "~1.0"
        }
    }

Next, update Composer from the Terminal:

    composer update

Then enable it in your suite configuration with the following settings

## Configuration

The configuration settings depending on which queueing service is being used, all the options are listed
here. Refer to the configuration examples below to identify the configuration options required for your chosen
service.

* service - the messaging service.
* token - API token and/or Access Token.
* room - The room/channel id for the messaging service.

> N.B. The API key for HipChat must be an users API token in order to provide sufficient access the last messages in
> a given room, however if you are just looking to send a messages to the service a room API token will be
> sufficient to send the message. Consult the HipChat API documentation for clarification on this topic.

## Examples
### Example Configuration (hipchat)

     modules:
       enabled: [IM]
        config:
           IM:
              service: 'hipchat'
              token: API_TOKEN
              room: ROOM_ID
              
### Example Usage

```php
<?php
$I = new IMGuy($scenario);
$I->wantTo('grab the recent messages on the IM server and run some tests');

$message = $I->grabLastInstantMessage();
$I->seeInLastInstantMessageFrom('Tester');
$I->dontSeeInLastInstantMessageFrom('Codeception');
$I->seeInLastInstantMessageContent('Testing has been completed with no issues.');
$I->dontSeeInLastInstantMessageContent('Random Message not there');
$I->seeInLastInstantMessageColor('yello');
$I->dontSeeInLastInstantMessageColor('red');
$date = $I->grabLastInstantMessageDate();
$I->seeInLastInstantMessageDate('2014-10-21T16:41:48.657455+00:00');
$I->dontSeeInLastInstantMessageDate('2015-10-21T16:41:48.657455+00:00');

$I->sendInstantMessage("Testing has been completed with no issues.", array('color' => 'yellow', 'notify' => true));
```

## Actions

TBA

# License

Released under the same license as Codeception: MIT