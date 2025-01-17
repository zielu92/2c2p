# Laravel 2C2P Payment Gateway

[![Latest Version on Packagist](https://img.shields.io/packagist/v/laraditz/2c2p.svg?style=flat-square)](https://packagist.org/packages/laraditz/2c2p)
[![Total Downloads](https://img.shields.io/packagist/dt/laraditz/2c2p.svg?style=flat-square)](https://packagist.org/packages/laraditz/2c2p)
[![License](https://poser.pugx.org/laraditz/2c2p/license?format=flat-square)](https://packagist.org/packages/laraditz/2c2p)

Simple laravel package for 2C2P Payment Gateway.

## Installation

You can install the package via composer:

```bash
composer require laraditz/2c2p
```

## Available Methods

Below are all methods available under this package.

| Method name               | Description  
|---------------------------|---------------------------------|
| createPayment()           | Create a new payment and get payment URL.  

## Usage

You can use service container or facade.
```php
// Using service container
app('Twoc2p')->createPayment($data);

// Using facade
\Twoc2p::createPayment($data);

```

### Create Payment
To create payment and get the payment URL to be redirected to.

| Parameter                 |   Type    | Description  
|---------------------------|:---------:|-----------------------|
| invoiceNo                 | string    | Unique invoice Number
| description               | string    | Description of the payment
| amount                    | decimal   | The amount of payment
| frontendReturnUrl         | string    | Redirect to this URL once payment complete

Example as below:
```php
app('Twoc2p')->createPayment([
    'invoiceNo' => '1523953661',   
    'description' => 'item 1',
    'amount' => 100.00,
    'frontendReturnUrl' => 'http://domain.test/your-return-url',
]);
```

Return example:
```php
array:2 [
  "id" => "94a19a34-965a-4e11-acd2-7acb02696f18"
  "payment_url" => "https://sandbox-pgw-ui.2c2p.com/payment/4.1/#/token/kSAops9Zwhos8hSTSeLTUxxx"
]
```

Redirect to the `payment_url` to proceed to 2C2P payment page. Once done, you will be redirected to the `frontendReturnUrl`. Below is the sample response returned.
```php
{
	"invoiceNo": "280520075921",
	"channelCode": "CC",
	"respCode": "2000",
	"respDesc": "Transaction is completed, please do payment inquiry request for full payment information."
}
```

## Event

This package also provide some events to allow your application to listen to it. You can create your listener and register it under event below.

| Event                                     |  Description  
|-------------------------------------------|-----------------------|
| Laraditz\Twoc2p\Events\BackendReceived    | Received backend response from 2C2P for a payment. Can use to update your payment status and other details


### Changelog

Please see [CHANGELOG](CHANGELOG.md) for more information what has changed recently.

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) for details.

### Security

If you discover any security related issues, please email raditzfarhan@gmail.com instead of using the issue tracker.

## Credits

-   [Raditz Farhan](https://github.com/laraditz)

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.