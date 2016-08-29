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

+ ```{% comment %}```
+ ```{% raw %}```
+ ```{% if %}```
+ ```{% unless %}```
+ ```{% case %}```
+ ```{% cycle %}```
+ ```{% for %}```
+ ```{% tablerow %}```
+ ```{% assign %}```
+ ```{% increment %}```
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
```{% decrement %}```
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
	```{% capture %}```
	```{% include %}```


## Operators

## Arrays

## Images

## Loops

## Pagination