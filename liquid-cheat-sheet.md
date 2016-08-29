# Liquid Cheat Sheet

## Template Variables

+ Product
+ Collection
+ Cart
+ Pages
+ Linklist
+ Blog
+ Article
+ Images
+ Customers
+ Shop

## Liquid Filters

## Liquid Logic

+ ```{% assign %}```
+ ```{% comment %}```
	* This tag allows you to put comments in your liquid code. 
	```
	{% comment %} This is a great comment {% endcomment %}
	```
+ ```{% case %}```
+ ```{% cycle %}```
+ ```{% capture %}```
+ ```{% decrement %}```
	* decrement sets the variable to 0, then every time it is called after, it decrements the variable by 1.  It works independently of variables created using the ```assign``` or ```capture``` keywords even if they have the same name.
	```
	{% increment counter %}
	{% increment counter %}
	{% increment counter %}

	{{ counter }}

	returns 

	- 1
	- 2
	- 3

	- 3
	```
+ ```{% for %}```
+ ```{% if %}```
+ ```{% include %}``` 
+ ```{% increment %}```
	+ increment sets the variable to 0, then every time it is called after, it increments the variable by 1.  It works independently of variables created using the ```assign``` or ```capture``` keywords even if they have the same name.
	
	```
	{% increment counter %}
	{% increment counter %}
	{% increment counter %}

	{{ counter }}

	returns 

	0
	1
	2
	
	2
	```
+ ```{% raw %}```
	* disable liquid processing engine using the raw tag.
	```
	{% raw %}{% assign var = 'this'%}{% endraw %}

	returns

	{% assign var = 'this'%}
	```
+ ```{% unless %}```
+ ```{% tablerow %}```




## Operators

## Arrays

## Images

## Loops

## Forms
	```{% form 'name_of_shopify_form' %}```
	* activate_customer_password
	* new_comment
	* contact
	* customer
	* create_customer
	* customer_address
	* customer_login
	* guest_login
	* recover_customer_password
	* reset_customer_password
	* storefront_password



## Pagination