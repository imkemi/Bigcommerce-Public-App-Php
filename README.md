# Bigcommerce-Public-App-Php
Connect PHP applications with the Bigcommerce Platform https://developer.bigcommerce.com
Bigcommerce API Client
======================

PHP client for connecting to the Bigcommerce V2 REST API.

Requirements for this connection
------------

- PHP 5.3 or greater
- cUrl extension enabled

**To connect to the API with OAuth you will need the following:**

- client_id
- auth_token
- store_hash

Installation
------------

Use the following Composer command to install the
API client from [the Bigcommerce vendor on Packagist](https://packagist.org/packages/bigcommerce/api):

~~~shell
 $ composer require bigcommerce/api
 $ composer update
~~~

You can also install composer for your specific project by running the following in the library folder.

~~~shell
 $ curl -sS https://getcomposer.org/installer | php
 $ php composer.phar install
 $ composer install
~~~
***********************************************************************************
In this file i have upload the vendor file so no need to install  composer
***********************************************************************************

Configuration
-------------

To use the API client in your PHP code, ensure that you can access `Bigcommerce\Api`
in your autoload path (using Composer’s `vendor/autoload.php` hook is recommended).

Provide your credentials to the static configuration hook to prepare the API client
for connecting to a store on the Bigcommerce platform:

### OAuth
~~~php
Bigcommerce::configure(array(
    'client_id' => 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx', // Ex.ufrfhuf67ffr7frf7hrfrfyrfgmu
    'auth_token' => 'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx', // Ex. 7rt7yrt7g7frfryfffdv7yfyr7f
    'store_hash' => 'xxxxxxxxxxxxxxx' // Ex. 4huy6fyr7
));
~~~

Connecting to the store
-----------------------

To test that your configuration was correct and you can successfully connect to
the store, ping the getTime method which will return a DateTime object
representing the current timestamp of the store if successful or false if
unsuccessful:

Accessing collections and resources (GET)
-----------------------------------------

To list all the resources in a collection:

~~~php
$products = Bigcommerce::getProducts();

foreach ($products as $product) {
	echo $product->name;
	echo $product->price;
}
~~~

To view the total count of resources in a collection:

~~~php
$count = Bigcommerce::getProductsCount();

echo $count;
~~~

Updating existing resources (PUT)
---------------------------------

To update a single resource:

~~~php
$product = Bigcommerce::getProduct(31);

$product->name = "Sumsung Galexy Note";
$product->price = 599.95;
$product->update();
~~~

You can also update a resource by passing an array or stdClass object of fields
you want to change to the global update method:

~~~php
$fields = array(
	"name"  => "Sumsung Galexy Note",
	"price" => 999.95
);

Bigcommerce::updateProduct(16, $fields);
~~~

Creating new resources (POST)
-----------------------------
$fields = array(
	"name" => "Iphone 6s"
);

Bigcommerce::createProduct($fields);

Deleting resources and collections (DELETE)
-------------------------------------------

To delete a single resource you can call the delete method on the resource object:

~~~php
$category = Bigcommerce::getCategory(50);
$category->delete();
~~~

