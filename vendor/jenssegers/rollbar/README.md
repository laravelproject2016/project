Laravel Rollbar
===============

[![Build Status](http://img.shields.io/travis/jenssegers/laravel-rollbar.svg)](https://travis-ci.org/jenssegers/laravel-rollbar) [![Coverage Status](http://img.shields.io/coveralls/jenssegers/laravel-rollbar.svg)](https://coveralls.io/r/jenssegers/laravel-rollbar)

Rollbar error monitoring integration for Laravel projects. This library adds a listener to Laravel's logging component. Laravel's session information will be sent in to Rollbar, as well as some other helpful information such as 'environment', 'server', and 'session'.

![rollbar](https://d37gvrvc0wt4s1.cloudfront.net/static/img/features-dashboard1.png?ts=1361907905)

Installation
------------

Install using composer:

    composer require jenssegers/rollbar

Add the service provider in `app/config/app.php`:

    'Jenssegers\Rollbar\RollbarServiceProvider',

Configuration
-------------

This package supports configuration through the services configuration file located in `app/config/services.php`. All configuration variables will be directly passed to Rollbar:

    'rollbar' => array(
        'access_token' => 'your-rollbar-token',
        'level' => 'debug'
    ),

The level variable defines the minimum log level at which log messages are sent to Rollbar. For development you could set this either to `debug` to send all log messages, or to `none` to sent no messages at all. For production you could set this to `error` so that all info and debug messages are ignored.

Usage
-----

To monitor exceptions, simply use the `Log` facade:

    App::error(function(Exception $exception, $code)
    {
        Log::error($exception);
    });

Your other log messages will also be sent to Rollbar:

    Log::debug('Here is some debug information');

### Context informaton

You can pass user information as context like this:

    Log::error('Something went wrong', [
        'person' => ['id' => 123, name' => 'John Doe', 'email' => 'john@doe.com']
    ]);

Or pass some extra information:

    Log::warning('Something went wrong', [
        'download_size' => 3432425235
    ]);
