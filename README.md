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
### sendInstantMessage
Simple method for sending a messages to an messaging service.

```php
<?php
$I->sendInstantMessage('Testing message to be send to IM service.', array('color' => 'red', 'notify' => true);
?>
```

* Param string $message Message to be sent.
* Param array $options Depends on service, for HipChat these include the color and the notify option.

### grabLastInstantMessage
Grabber method to return the last messages on the service.

```php
<?php
$messages = $I->grabLastInstantMessage();
?>
```

### grabLastInstantMessageFrom
Grabber method to return the from field of the last message.

```php
<?php
$from = $this->grabLastInstantMessageFrom();
?>
```
     
### seeInLastInstantMessageFrom
Checks whether the last messages from address matches.

```php
<?php
$I->seeInLastInstantMessageFrom('Codeception');
?>
```
     
### dontSeeInLastInstantMessageFrom
Checks whether the last messages from address does not match.

```php
<?php
$I->dontSeeInLastInstantMessageFrom('Codeception');
?>
```

### grabLastInstantMessageContent
Grabber method to return the content/text of the last message.

```php
<?php
$from = $this->grabLastInstantMessageContent();
?>
```
      
### seeInLastInstantMessageContent
Checks whether the last messages content/text matches.

```php
<?php
$I->seeInLastInstantMessageContent('Hello this is the messages I am expecting to see.');
?>
```

### dontSeeInLastInstantMessageContent
Checks whether the last messages content/text does not match.

```php
<?php
$I->dontSeeInLastInstantMessageContent('Hello this is the messages I am not expecting to see.');
?>
```

### grabLastInstantMessageColor
Grabber method to return the color of the last message.

```php
<?php
$from = $this->grabLastInstantMessageColor();
?>
```

### seeInLastInstantMessageColor
Checks whether the last messages color matches.

```php
<?php
$I->seeInLastInstantMessageColor('red');
?>
```

### dontSeeInLastInstantMessageColor
Checks whether the last messages color does not match.

```php
<?php
$I->dontSeeInLastInstantMessageColor('red');
?>
```

### grabLastInstantMessageDate
Grabber method to return the date/time of the last message.

```php
<?php
$from = $this->grabLastInstantMessageDate();
?>
```

### seeInLastInstantMessageDate
Checks whether the last messages date matches.

```php
<?php
$I->seeInLastInstantMessageDate('2014-10-13T16:30:48.657455+00:00');
?>
```

### dontSeeInLastInstantMessageDate
Checks whether the last messages date does not match.

```php
<?php
$I->dontSeeInLastInstantMessageDate('2015-11-13T16:30:48.657455+00:00');
?>
```

# License

Released under the same license as Codeception: MIT