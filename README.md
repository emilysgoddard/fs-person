# fs-person




`fs-person` is a FamilySearch web component that displays a person's name, lifespan, and person id (PID). By default, the element displays the person's full name on one line, and their vital information on the next line. Their vital information is displayed with the lifespan first and the PID second, with a dot separating them.




The component retrieves the person's data either through the `pid` or the `object` attribute that the consumer specified on the element. If both attributes are included on the element, it will default to using the `pid`.




The component can be customized in several ways. In addition to its default display, the person's name can be displayed as a link, as a heading, or both. The pid and the lifespan can both be hidden if desired. Also, the lifespan can be displayed as a long lifespan (e.g., displaying "31 October 1902 – 2 May 1987" instead of "1902–1987").




The component can also be styled by wrapping it in a `div` that has one or more of these style classes applied to it: `fs-person--light`, `fs-person--dark`, `fs-person--inline`, or `fs-person--stacked`. These styles are inherited from the FamilySearch global style guide. All of the general styling of the `fs-person` element is inherited from the FamilySearch global style guide as well.




## Usage








The `fs-person` web component can be installed with Bower.
```
bower install --save fs-webdev/fs-styles
```




```html
//Importing the fs-person component into your document
<link rel="import" href="bower_components/fs-styles/fs-person/fs-person.html">




//Rendering a person by passing in a person id (PID)
<fs-person pid='XXXX-XXX'></fs-person>




//Rendering a person by passing in an object
<fs-person object='{...}'></fs-person>
```




## Attributes




* `pid` - A string that is formatted with four alphanumeric characters, a dash, and then three more alphanumeric characters (e.g., "J3N9-2J0"). The `pid` is used fetch the person's data and pass it to the web component. It is also a property that can be accessed and updated using `this.pid`.
* `object` - A string containing an object that has all the data necessary to render the person. If the object is not passed in as a string, the data will be rendered as "Invalid Person." `object` is also a property that can be accessed and updated using `this.object`. The object is expected to be in the following format:




*(Required keys: `id`, `summary`, `summary.nameForms`, `living`, `lifespan`)*
```json
{
	"id": "5XG4-L2Y",
	"summary": {
		"name": "John Doe",
		"nameForms": [
			{
				"lang": "x-Latn"
			}
		],
		"living": false,
		"lifespan": "1902–1987",
		"lifespanBegin": {
			"date": {
				"normalized": [
					{
						"value": "31 October 1902"
					}
				]
			}
		},
		"lifespanEnd": {
			"date": {
				"normalized": [
					{
						"value": "2 May 1987"
					}
				]
			}
		}
	},
	"givenName": "John",
	"familyName": "Doe"
}
```




*Note: `object.summary.lifespanBegin` and `object.summary.lifespanEnd` are optional, and only need to be included in the object if the `longLifespan` attribute is used.*




* `longLifespan` - A boolean that will display the lifespan as a "long lifespan" if that data is available (e.g., displays "31 October 1902 - 2 May 1987" instead of "1902-1987").
* `noPid` - A permanent boolean attribute that cannot be toggled on and off. If this attribute is included, the pid will not be displayed. 
* `noLifespan` - A permanent boolean attribute that cannot be toggled on and off. If this attribute is included, the lifespan will not be displayed. 
* `noDetails` - A permanent boolean attribute that cannot be toggled on and off. If this attribute is included, none of the person's vital information will be displayed. 
* `heading` - A string containing the desired heading level. Example:
```html
<fs-person pid='XXXX-XXX' heading='h2'></fs-person>
```
* `link` A string containing the desired link or web address. Example:
```html
<fs-person pid='XXXX-XXX' link='#'></fs-person>
```
## Events
* `load` - Fires after the renderPerson function is done. This event does not bubble.
* `fs-person-load` - Fires after the renderPerson function is done. This event bubbles.
* `error` - Fires when something goes wrong  (e.g., if an invalid object or pid is passed in). This event does not bubble.
* `fs-person-error` - Fires when something goes wrong (e.g., if an invalid object or pid is passed in). This event bubbles.




## Bad Data


When bad data is passed in, `fs-person` throws an error but continues to render the person as an "invalid person" object. The person's name will be displayed as "Invalid Person" and their lifespan will be displayed as "0000–0000." If a PID was passed in, the component will display it as it was given; otherwise, the PID will display as "0000-000."
