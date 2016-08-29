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
+ Array filters
	* join
	* first
	* last
	* concat
	* index
	* map
	* reverse
	* size
	* sort
	* uniq
+ HTML filters
	* image_tag
	* script_tag
	* stylesheet_tag
+ Math filters
	* abs
	* ceil
	* divided_by
	* floor
	* minus
	* plus
	* round
	* times
	* modulo
+ Money filters
	* money
	* money_with_currency
	* money_without_trailing_zeros
	* money_without_currency
+ String filters
	* append
		- Appends characters to a string.
		```
		{{ 'book' | append: '.png' }}

		returns

		book.png
		```
	* camelcase
		- Converts a string into CamelCase.
		```
		{{ 'this-is-awesome' | camelcase }}

		returns

		ThisIsAwesome
		```
	* capitalize
		- Capitalizes the first word in a string
		```
		{{ 'this is awesome' | capitalize }}

		returns

		This is awesome
		```
	* downcase
		- Converts a string into lowercase
		```
		{{ "THIS IS AWESOME" | downcase }}

		returns

		this is awesome
		```
	* escape
		- Escapes text.  For example prevents the <p> tags from rendering and they show up as a string.
		```
		{{ "<p>The book</p>" | escape }}

		returns

		<p>The book</p>
		```
	* handle/handleize
		- Takes a string and turns it into a slug.
		```
		{{ '100% M & Ms!!!' | handleize }}

		returns

		100-m-ms
		```
	* ### Encoding
	* md5
		- Converts a string into an MD5 hash.
	* sha1
		- Converts a string into a SHA-1 hash.
	* sha256
		- Converts a string into a SHA-256 hash
	* hmac_sha1
		- Converts a string into a SHA-1 hash using a hash message authentication code (HMAC).
	* hmac_sha256
		- Converts a string into a SHA-256 hash using a hash message authentication code (HMAC)
	* newline_to_br
		- Inserts a <br > linebreak HTML tag in front of each line break in a string.
		```
		{% capture var %}
		One Fish
		Two Fish
		Red Fish
		Blue Fish
		{% endcapture %}
		{{ var | newline_to_br }}

		returns

		One Fish<br>
		Two Fish<br>
		Red Fish<br>
		Blue Fish<br>
		```
	* pluralize
	* prepend
	* remove
	* remove_first
	* replace
	* replace_first
	* slice
	* split
	* strip
	* lstrip
	* rstrip
	* strip_hmtl
	* strip_newlines
	* truncate
	* truncatewords
	* upcase
	* url_encode
	* url_escape
	* url_param_escape
	* reversing strings
+ URL filters
	* asset_url
	* asset_img_url
	* file_url
	* file_img_url
	* customer_login_link
	* global_asset_url
	* img_url
	* link_to
	* link_to_vendor
	* link_to_type
		- Creates an HTML link to a collection page that lists all products belonging to a product type.
		```
		{{ "postcards" | link_to_type }}

		returns

		<a href="/collections/types?q=postcards" title="postcards">postcards</a>
		```
	* link_to_tag
	* link_to_add_tag
	* link_to_remove_tag
	* payment_type_img_url
	* product_img_url
	* collection_img_url
	* shopify_asset_url
	* url_for_type
	* url_for_vendor
	* within
+ Additional filters
	* date
	* default
	* default_errors
	* default_pagination
	* hex_to_rgba
	* highlight_active_tag
	* json
	* weight_with_unit

## Liquid Logic


### Variable tags
+ assign
	* ```{% assign %}```
		- Creates a new variable.
		```
		{% assign var-name = 'elephant' %}
		{{ var-name }}

		returns

		elephant
		```
+ capture
	* ```{% capture %}```
		- Captures the string inside of the opening and closing tags and assigns it to a variable. Variables created through {% capture %} are strings. This is very useful for capturing information that's being looped over.
		```
		{% capture item_list %}
		  {% for item in cart.items %}
		      {{ item.product.title }}
		  {% endfor %}
		{% endcapture %}

		returns

		item1 item2 item3
		```
		assuming those are the items in your cart.
+ increment
	* ```{% increment %}```
		* increment sets the variable to 0, then every time it is called after, it increments the variable by 1.  It works independently of variables created using the ```assign``` or ```capture``` keywords even if they have the same name.
		
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
+ decrement
	* ```{% decrement %}```
		- decrement sets the variable to 0, then every time it is called after, it decrements the variable by 1.  It works independently of variables created using the ```assign``` or ```capture``` keywords even if they have the same name.
		```
		{% increment counter %}
		{% increment counter %}
		{% increment counter %}

		{{ counter }}

		returns 

		+ 1
		+ 2
		+ 3

		+ 3
		```

### Iteration tags
+ for
	+ ```{% for %}```
	+ Repeatedly executes a block of code.
	```
	{% for product in collection.products %}
	  {{ product.title }}
	{% endfor %}
	```

	+ for loops can output a maximum of 50 results per page. In cases where there are more than 50 results, use the paginate tag to split them across multiple pages.

+ cycle
	+ ```{% cycle %}```
	+ Loops through a group of strings and outputs them in the order that they were passed as parameters. Each time cycle is called, the next string that was passed as a parameter is output. In this example we're using it to add the class of last to every fourth div.
	```
	<div class="left {% cycle '','','','last' %}">
	      <img src="{{ product.featured_image.src | product_img_url: 'medium' }}" />
	</div>

	returns

	<div class="left"></div>
	<div class="left"></div>
	<div class="left"></div>
	<div class="left last"></div>
	<div class="left"></div>
	<div class="left"></div>
	<div class="left"></div>
	<div class="left last"></div>

	```
+ tablerow
	+ ```{% tablerow %}```
	+ Generates an HTML <table>. Must be wrapped in an opening <table> and closing </table> HTML tags.
	```
	<table>
	{% tablerow product in collection.products %}
	  {{ product.title }}
	{% endtablerow %}
	</table>

	returns

	<table>
	    <tr class="row1">
	        <td class="col1">
	            the blue book
	        </td>
	        <td class="col2">
	            the red book
	        </td>
	        <td class="col3">
	            the yellow book
	        </td>
	    </tr>
	</table>
	```
	+ You can add the 'cols' parameter to affect how many there are in a row
	```
	{% tablerow product in collection.products cols:2 %}
	  {{ product.title }}
	{% endtablerow %}

	returns

	<table>
	    <tr class="row1">
	        <td class="col1">
	            the blue book
	        </td>
	        <td class="col2">
	            the red book
	        </td>
	    </tr>
	    <tr class="row2">
	        <td class="col1">
	            the yellow book
	        </td>
	    </tr>
	</table>
	```


### Control flow tags
+ if
	* ```{% if %}```
		- Acts as a standard if statement and executes a block of code only if a certain condition is met
		```
		{% if product.title == 'the blue book' %}
		  You are buying the blue book!
		{% endif %}
		```
		- Also can use ```{% elsif %}``` and ```{% else %}``` in conjunction with this statement.
+ unless
	* ```{% unless %}```
		- Like if, but executes a block of code only if a certain condition is not met (ie. result is false).
		```
		{% unless product.title == 'the blue book' %}
		  You are NOT buying the blue book!
		{% endunless %}
		```
+ case
	* ```{% case %}```
		- Creates a switch statement to execute a particular block of code when a variable has a specified value. **case** initializes the switch statement, and **when** statements define the various conditions. The **else** statement is used as a catchall to execute if none of the conditions are met.
		```
		{% case product.title %}
		  {% when 'The blue book' %}
		     You're getting the blue book
		  {% when 'The red book' %}
		    You're getting the red book
		  {% else %}
		     You're getting another color book
		{% endcase %}
		```

### Theme tags
+ comment
	* ```{% comment %}```

		- This tag allows you to put comments in your liquid code. 
		```
		{% comment %} This is a great comment {% endcomment %}
		```
+ include
	* ```{% include %}``` 
		- Inserts a snippet from the snippets folder of a theme.

		```{% include 'snippet-name' %}```

		- You can also include variables to be used within the snippet.

		```{% include 'snippet', first_var: 'books', second_var: 'videos' %}```

		- The with parameter assigns a value to a variable inside a snippet that shares the same name as the snippet. If snippet is named 'fruit.liquid' you can use:

		```{% include 'fruit' with 'peach' %}```

			- this will set the variable fruit inside the snippet to 'peach'.
+ form
	* ```{% form %}```
		- Shopify creates some helpers in order to make standard forms for your shop. Please see the *Forms* section for more detail.
+ layout
+ paginate
+ raw
	* ```{% raw %}```
		- disable liquid processing engine using the raw tag.
		```
		{% raw %}{% assign var = 'this'%}{% endraw %}

		returns

		{% assign var = 'this'%}
		```




## Operators

## Arrays

## Images

## Loops
### [forloop helpers](https://help.shopify.com/themes/liquid/objects/for-loops) 

## Forms
Shopify creates some helpers in order to make standard forms for your shop.

```{% form 'name_of_shopify_form' %}```
+ **activate_customer_password**
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
+ **new_comment**
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
+ **contact**
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
+ **customer**
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
+ **create_customer**
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
+ **customer_address**
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
+ **customer_login**
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
+ **guest_login**
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
+ **recover_customer_password**
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
+ **reset_customer_password**
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
+ **storefront_password**
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