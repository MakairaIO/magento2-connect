# Makaira Headless Extension for Magento 2

[![Packagist Version](https://img.shields.io/packagist/v/makaira/magento2-connect)](https://packagist.org/packages/makaira/magento2-connect)
[![Build Status](https://travis-ci.org/makaira/magento2-connect.svg?branch=main)](https://travis-ci.org/makaira/magento2-connect)

This document helps you integrate the Makaira Headless Extension into your Magento 2 Shop.

## Table of contents
- [Requirements](#requirements)
- [Installation](#installation)
- [Activating the Module](#activating-the-module)
- [API endpoint examples](#api-endpoint-examples)

## Requirements

This module supports:

- Magento 2 version 2.2 and higher
- PHP version 7.1 and higher  
  **Warning**: PHP 7.0 is not supported

## Installation

To install module, open your terminal and run the command:

    composer require codekunst/magento2-makaira:dev-main

Refer to Composer manual for more information. If, for some reason, `composer` is not available globally, proceed to install it following the
instructions available on the [project website](https://getcomposer.org/doc/00-intro.md).

## Activating the Module

From the root of your Magento 2 installation, enter these commands in sequence:

    php bin/magento module:enable Makaira_Headless
    php bin/magento setup:upgrade

As a final step, check the module activation by running:

    php bin/magento module:status

The module should now appear in the upper list *List of enabled modules*.

That's it, you are ready to go!

## API endpoint examples

All examples below are of content type `application/json`. PUT, DELETE and POST methods require a raw body with valid JSON. 

### Cart actions

Get all cart articles

    GET /makaira/cart/
    
    Response:
    {
        "success": true,
        "cart": {
            "items": [],
            "total": 0
        }
    }

Add article to cart

    POST /makaira/cart/
    
    Body:
    {
        "sku": "24-MB04",
        "quantity": "1"
    }
    
    Response:
    {
        "success": true,
        "cart": {
            "items": [
                {
                    "sku": "24-MB04",
                    "name": "Strive Shoulder Pack",
                    "quantity": 1,
                    "price": 32
                }
            ],
            "total": 32
        }
    }

Delete article from cart

    DELETE /makaira/cart/
    
    Body:
    {
        "sku": "24-MB04"
    }
    
    Response:
    {
        "success": true,
        "message": "Der Artikel wurde entfernt.",
        "sku": "24-MB04"
    }

Change article quantity in cart

    PUT /makaira/cart/
    
    Body:
    {
        "sku": "24-MB04",
        "quantity": "3"
    }
    
    Response:
    {
        "success": true,
        "cart": {
            "items": [
                {
                    "sku": "24-MB04",
                    "name": "Strive Shoulder Pack",
                    "quantity": 3,
                    "price": 32
                }
            ],
            "total": 96
        }
    }

### User actions

Get currently logged in user

    GET /makaira/user/
    
    Response:
    {
        "success": true,
        "user": null
    }
