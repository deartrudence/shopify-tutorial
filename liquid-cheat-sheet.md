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
Shopify creates some helpers in order to make standard forms for your shop
```{% form 'name_of_shopify_form' %}```
+ activate_customer_password
	* Generates a form for activating a customer account on the activate_account.liquid template.
	```
	{% for 'activate_customer_password %}
	...
	{% endform %}

	returns

	<form accept-charset="UTF-8" action="https://my-shop.myshopify.com/account/activate" method="post">
	  <input name="form_type" type="hidden" value="activate_customer_password" />
	  <input name="utf8" type="hidden" value="✓" />
	  ...
	</form>
	```
+ new_comment
	* Generates a form for creating a new comment in the article.liquid template. Requires the article object as a parameter.
	```
	{% form 'new_comment', article %}
	...
	{% endform %}

	returns 

	<form accept-charset="UTF-8" action="/blogs/news/10582441-my-article/comments" class="comment-form" id="article-10582441-comment-form" method="post">
	  <input name="form_type" type="hidden" value="new_comment" />
	  <input name="utf8" type="hidden" value="✓" />
	  ...
	</form>
	```
+ contact
	* Generates a form for submitting an email through the Liquid contact form.
	```
	{% form 'contact' %}
	...
	{% endform %}

	returns

	<form accept-charset="UTF-8" action="/contact" class="contact-form" method="post">
	  <input name="form_type" type="hidden" value="contact" />
	  <input name="utf8" type="hidden" value="✓" />
	  ...
	</form>
	```
+ customer
	* Generates a form for creating a new customer without registering a new account. This form is useful for collecting customer information when you don't want customers to log in to your store, such as building a list of emails from a newsletter signup.

	To generate a form that registers a customer account, use the create_customer form.
	```
	{% form 'customer' %}
	...
	{% endform %}

	returns

	<form method="post" action="/contact#contact_form" id="contact_form" class="contact-form" accept-charset="UTF-8">
	  <input type="hidden" value="customer" name="form_type">
	  <input type="hidden" name="utf8" value="✓">
	  ...
	</form>
	```
+ create_customer
	* Generates a form for creating a new customer account on the register.liquid template.
	```
	{% form 'create_customer' %}
	...
	{% endform %}

	returns

	<form accept-charset="UTF-8" action="https://my-shop.myshopify.com/account" id="create_customer" method="post">
	  <input name="form_type" type="hidden" value="create_customer" />
	  <input name="utf8" type="hidden" value="✓" />
	  ...
	</form>
	```
+ customer_address
	* Generates a form for creating or editing customer account addresses on the addresses.liquid template. When creating a new address, include the parameter customer.new_address. When editing an existing address, include the parameter address.
	```
	{% form 'customer_address', customer.new_address %}
	...
	{% endform %}

	returns

	<form accept-charset="UTF-8" action="/account/addresses/70359392" id="address_form_70359392" method="post">
	  <input name="form_type" type="hidden" value="customer_address" />
	  <input name="utf8" type="hidden" value="✓" />
	  ...
	</form>
	```
+ customer_login
	* Generates a form for logging into Customer Accounts on the login.liquid template.
	```
	{% form 'customer_login' %}
	...
	{% endform %}

	returns

	<form accept-charset="UTF-8" action="https://my-shop.myshopify.com/account/login" id="customer_login" method="post">
	  <input name="form_type" type="hidden" value="customer_login" />
	  <input name="utf8" type="hidden" value="✓" />
	  ...
	</form>
	```
+ guest_login
	* Generates a form on the login.liquid template that directs customers back to their checkout session as a guest instead of logging in to an account.
	```
	{% form 'guest_login' %}
	...
	{% endform %}

	returns

	<form method="post" action="https://my-shop.myshopify.com/account/login" id="customer_login_guest" accept-charset="UTF-8">
	  <input type="hidden" value="guest_login" name="form_type">
	  <input type="hidden" name="utf8" value="✓">
	  ...
	  <input type="hidden" name="guest" value="true">
	  <input type="hidden" name="checkout_url" value="https://checkout.shopify.com/store-id/checkouts/session-id?step=contact_information">
	</form>
	```
+ recover_customer_password
	* Generates a form for recovering a lost password on the login.liquid template.
	```
	{% form 'recover_customer_password' %}
	...
	{% endform %}

	returns

	<form accept-charset="UTF-8" action="/account/recover" method="post">
	  <input name="form_type" type="hidden" value="recover_customer_password" />
	  <input name="utf8" type="hidden" value="✓" />
	  ...
	</form>
	```
+ reset_customer_password
	* Generates a form on the customers/reset_password.liquid template for a customer to reset their password.
	```
	{% form 'reset_customer_password' %}
	...
	{% endform %}

	returns

	<form method="post" action="https://my-shop.myshopify.com/account/account/reset" accept-charset="UTF-8">
	  <input type="hidden" value="reset_customer_password" name="form_type" />
	  <input name="utf8" type="hidden" value="✓" />
	  ...
	  <input type="hidden" name="token" value="408b680ac218a77d0802457f054260b7-1452875227">
	  <input type="hidden" name="id" value="1080844568">
	</form>
	```
+ storefront_password
	* Generates a form on the password.liquid template for entering a password-protected storefront.
	```
	{% form 'storefront_password' %}
	...
	{% endform %}

	returns

	<form method="post" action="/password" id="login_form" class="storefront-password-form" accept-charset="UTF-8">
	  <input type="hidden" value="storefront_password" name="form_type">
	  <input type="hidden" name="utf8" value="✓">
	  ...
	</form>

	```


## Pagination