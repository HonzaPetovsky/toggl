ixudra/toggl
================

[![Latest Version on Packagist](https://img.shields.io/packagist/v/ixudra/toggl.svg?style=flat-square)](https://packagist.org/packages/ixudra/toggl)
[![license](https://img.shields.io/github/license/ixudra/toggl.svg)]()
[![Total Downloads](https://img.shields.io/packagist/dt/ixudra/toggl.svg?style=flat-square)](https://packagist.org/packages/ixudra/toggl)

Custom PHP library to connect with the Toggl API - developed by [Ixudra](https://ixudra.be).

This package can be used by anyone at any given time, but keep in mind that it is optimized for my personal custom workflow. It may not suit your project perfectly and modifications may be in order.



## Installation

Pull this package in through Composer.

```js

    {
        'require': {
            'ixudra/toggl': '2.*'
        }
    }

```

> Important: this package supports the latest version of the Toggle API (v9). If you want so use v8 of the API (soon to be deprecated), pull in version `1.2.0` instead.



### Laravel Integration

#### Laravel 5.5+

Automatic package discovery will take care of registering the
service provider and facade.

#### Laravel < 5.5

Add the service provider to your `config/app.php` file

```php

    'providers'         => array(

        //...
        Ixudra\Toggl\TogglServiceProvider::class,

    ),

```

Add the facade to your `config/app.php` file:

```php

    'aliases'           => array(

        //...
        'Toggl'         => Ixudra\Toggl\Facades\Toggl::class,

    ),

```

#### Configuration

Add workspace ID and your personal API token to your `.env` file:

```

TOGGL_WORKSPACE=123
TOGGL_TOKEN=your_toggl_api_token

```

Add the following lines of code to your `config/services.php` file:

```php

    'toggl' => [
        'workspace'     => env('TOGGL_WORKSPACE'),
        'token'         => env('TOGGL_TOKEN'),
    ],

```

The credentials in the configuration file will be used as the default for the package. If for whatever reason you would like to use a different workspace ID and/or API token, you can do so using two utility methods. You can use either one, none or both, depending on your personal needs:

```php

    // Sets the workspace ID to a new value
    Toggl::setWorkspaceId( 456 );
    // Sets the API token to a new value       
    Toggl::setApiToken( 'second_toggl_api_token' );
    
    $response = Toggl::createClient( array( 'name' => 'Test company' ) );

```

 > Keep in mind that the workspace ID and API token are stored in the service configuration. This means that once one of these values is updated, it will not go back to the default once the next request is completed. It will keep the new value until it is reset to it's original value using the same utility methods.


### Lumen 5.* integration

In your `bootstrap/app.php`, make sure you've un-commented the following line (around line 26):

```
$app->withFacades();
```

Then, register your class alias:
```
class_alias('Ixudra\Toggl\Facades\Toggl', 'Toggl');
```

Finally, you have to register your ServiceProvider (around line 70-80):

```
/*
|--------------------------------------------------------------------------
| Register Service Providers
|--------------------------------------------------------------------------
|
| Here we will register all of the application's service providers which
| are used to bind services into the container. Service providers are
| totally optional, so you are not required to uncomment this line.
|
*/

// $app->register('App\Providers\AppServiceProvider');

// Package service providers
$app->register(Ixudra\Toggl\TogglServiceProvider::class);
```


### Integration without Laravel

Create a new instance of the `TogglService` where you would like to use the package:

```php

    $workspaceId = 123;
    $apiToken = 'your_toggl_api_token';
    $togglService = new \Ixudra\Toggl\TogglService( $workspaceId, $apiToken );

```



## Usage

The package provides an easy interface for sending requests to the Toggl API. For the full information regarding the API,
all available methods and all possible parameters, I would refer you to the official Toggl API documentation on 
[GitHub](https://github.com/toggl/toggl_api_docs). The package provides a (nearly) exact match of (almost) all the functions that are described
in the API documentation. The exact function definitions can be found in the `src/Traits` directory.

For your convenience, the package will automatically add several required parameters, so you don't have to worry about 
doing so. These parameters include the workspace ID and the API token. These parameters should not be included in any
of the requests. Additionally, the package also provides several utility methods for the 


### Laravel usage

```php

    // Return an overview of what users in the workspace are doing and have been doing
    $response = Toggl::dashboard();

    // Create a client
    $response = Toggl::createClient( array( 'name' => 'Test company' ) );

    // Get a summary information of this month for all user 
    $response = Toggl::summaryThisMonth();

    // Get a summary information of last month for one specific user 
    $response = Toggl::summaryLastMonth( array( 'user_ids' => '123' ) );

```


### Non-laravel usage

```php

    $workspaceId = 123;
    $apiToken = 'your_toggl_api_token';
    $togglService = new \Ixudra\Toggl\TogglService( $workspaceId, $apiToken );

    // Return an overview of what users in the workspace are doing and have been doing
    $response = $togglService->dashboard();

    // Create a client
    $response = $togglService->createClient( array( 'name' => 'Test company' ) );

    // Get a summary information of this month for all user 
    $response = $togglService->summaryThisMonth();

    // Get a summary information of last month for one specific user 
    $response = $togglService->summaryLastMonth( array( 'user_ids' => '123' ) );

```




## Planning

- Add missing API methods
- Improve usability of existing API methods
- Add additional convenience method
- Update and improve documentation
- Support for multiple workspaces




## Support

Help me further develop and maintain this package by supporting me via [Patreon](https://www.patreon.com/ixudra)!!




## License

This package is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT)




## Contact

For package questions, bug, suggestions and/or feature requests, please use the GitHub issue system and/or submit a pull request. When submitting an issue, always provide a detailed explanation of your problem, any response or feedback your get, log messages that might be relevant as well as a source code example that demonstrates the problem. If not, I will most likely not be able to help you with your problem. Please review the [contribution guidelines](https://github.com/ixudra/toggl/blob/master/CONTRIBUTING.md) before submitting your issue or pull request.

For any other questions, feel free to use the credentials listed below: 

Jan Oris (developer)

- Email: jan.oris@ixudra.be
- Telephone: +32 496 94 20 57
