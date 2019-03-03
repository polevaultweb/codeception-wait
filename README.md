Codeception Wait
==========

A utility library, designed to help the user to wait until a condition turns true.

## Installation
You need to add the repository into your composer.json file

```bash
    composer require --dev polevaultweb/codeception-wait
```

## Usage

In your custom module add a method:

```php
/**
 * @param int $timeout_in_second
 * @param int $interval_in_millisecond
 *
 * @return ModuleWait
 */
protected function wait( $timeout_in_second = 30, $interval_in_millisecond = 250 ) {
    return new ModuleWait( $this, $timeout_in_second, $interval_in_millisecond );
}
```

Then you can create a condition and wait for it to happen, e.g.

```php
/**
 * Wait until an email to be received.
 *
 * @param int $timeout
 *
 * @throws \Exception
 */
public function waitForEmail($timeout = 5)
{
    $condition = function () {
        $message = $this->fetchLastMessage();
        return ! empty( $message );
    };

    $message = sprintf('Waited for %d secs but no email has arrived', $timeout);

    $this->wait($timeout)->until($condition, $message);
}
```
