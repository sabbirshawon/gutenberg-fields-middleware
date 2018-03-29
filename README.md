# Gutenberg Fields Middleware

Provides middleware to easily register fields for Gutenberg blocks.



After activating the plugin use `gutenberg-fields-middleware` handle as dependency when enqueueing your block js file. Define your fields inside `attributes` as `field` and then use ( optionally ) those fields inside `edit` method as `middleware.fields.attributeKey` 



## Example Usage


```js
registerBlockType( 'example-namespace/example-block', {
	title: 'Example Block',
	description: 'Block Description',
	icon: 'universal-access-alt',
	category: 'common',
	attributes: {
		url: {
			type: 'string',
			field: {
				type: 'url',
			},
		},
		text: {
			type: 'string',
			field: {
				type: 'text',
				placeholder: 'Enter link text',
			},
		},
		image: {
			type: 'object',
			field: {
				type: 'image',
				buttonText: 'Upload',
				imagePlaceholder: true,
				removeButtonText: 'Remove',
			},
		},
		option: {
			type: 'string',
			field: {
				type: 'select',
				label: 'Select Numbers',
				options: [
					{
						value: 'one',
						label: 'one',
					},
					{
						value: 'two',
						label: 'two',
					},
				],
			},
		},
		radio: {
			type: 'string',
			field: {
				type: 'radio',
				options: [
					{
						value: 'one',
						label: 'one',
					},
					{
						value: 'two',
						label: 'two',
					},
				],
			},
		},
		number: {
			type: 'string',
			field: {
				type: 'number',
				label: 'Number',
				position: 'inspector',
			},
		},
		columns: {
			type: 'string',
			field: {
				type: 'range',
				position: 'inspector',
			},
		},
	},

	// Optional.
	edit( props, middleware ) {
		return [
			middleware.inspectorControls, // When adding inspector controls.
			middleware.fields.url,
			middleware.fields.text,
			middleware.fields.image,
			middleware.fields.option,
			middleware.fields.radio,
		];
	},

	save( props ) {
		return el(
			'div', {}, [
				el( 'p', {}, props.attributes.text ),
				el( 'a', { href: props.attributes.url }, 'Link' ),
				// ...
			]
		);
	},

} );
```



# Fields

Middleware has support for the following field types:



## text

Render an auto-growing textarea allow users to fill any textual content.

#### value:

The current value of text field.

- Type: `string`
- Required: No

#### onChange:

A function that receives the new value of the text field each time it changes.

- Type: `Function`
- Required: No

You can also pass any extra prop to the textarea rendered by this field. 

For more read gutenberg [readme.](https://github.com/WordPress/gutenberg/tree/master/blocks/plain-text)

**Example:**

```js
text: {
	type: 'string',
	field: {
		type: 'text',
		placeholder: __( 'Enter text' ),
	},
},
```



## rich-text

#### placeholder:

- Type: `String`
- Required: No

#### value:

The current value of rich text field.

- Type: `array`
- Required: No

#### onChange:

A function that receives the new value of the rich text field each time it changes.

- Type: `Function`
- Required: No

For full documentation read gutenberg [readme](https://github.com/WordPress/gutenberg/tree/master/blocks/rich-text).

**Example:**

```js
text: {
	type: 'string',
	field: {
		type: 'rich-text',
		placeholder: __( 'Enter text' ),
	},
},
```





## button

#### editable:

Make button editable.
* Type: `Bool`
* Required: No
* Default: false

#### buttonText:

Fallback button text.
* Type: `string`
* Required: No
* Default: null

#### isPrimary:

Button class. Other button classes are `isPrimary`, `isSmall`, `isToggled`, `isBusy`. Applicable only when `editable: true`  is not set.

* Type: `bool`
* Required: No
* Default: null

#### disabled:

- Type: `bool`
- Required: No
- Default: null

#### href:

If set, `button` will be replaced with `a`
* Type: `bool`
* Required: No
* Default: null


For more [read gutenberg readme](https://github.com/WordPress/gutenberg/tree/master/components/button).

**Example:**

```js
button: {
	type: 'string',
	field: {
		type: 'button',
		isLarge: true,
		editable: true,
	},
}
```



## radio

#### label:

If set, a label will be generated using label property as the content.
* Type: `String`
* Required: No

#### help:

If set, a help text will be generated using help property as the content.
* Type: `String`
* Required: No


#### selected:

The value property of the currently selected option.
* Type: `Object`
* Required: No

#### options:

An array of objects containing the following properties:
* label: (string) The label to be shown to the user.
* value: (Object) The internal value compared against select and passed to onChange.


* Type: `Array`
* Required: No

#### onChange:

A function that receives the value of the new option that is being selected as input.
* Type: `function`
* Required: No

For more [read gutenberg readme](https://github.com/WordPress/gutenberg/tree/master/components/radio-control).

**Example:**

```js
radio: {
	type: 'string',
	field: {
		type: 'radio',
		label: 'User type',
		help: 'The type of the current user',
		options: [
			{
				value: 'one',
				label: 'one',
			},
			{
				value: 'two',
				label: 'two',
			},
		],
	},
}
```



## checkbox

#### heading:

A heading for the input field, that appears above the checkbox. If the prop is not passed no heading will be rendered.
* Type: `String`
* Required: No

#### label:

A label for the input field, that appears at the side of the checkbox. The prop will be rendered as content a label element. If no prop is passed an empty label is rendered.
* Type: `String`
* Required: No


#### help:

If this property is added, a help text will be generated using help property as the content.
* Type: `String`
* Required: No

#### checked:

If checked is true the checkbox will be checked. If checked is false the checkbox will be unchecked. If no value is passed the checkbox will be unchecked.
* Type: `Boolean`
* Required: No

#### onChange:

A function that receives the checked state (boolean) as input.
* Type: `function`
* Required: Yes

For more [read gutenberg readme](https://github.com/WordPress/gutenberg/tree/master/components/checkbox-control).

**Example:**

```js
check: {
	type: 'boolean',
	field: {
		default: false,
		type: 'checkbox',
		heading: 'User',
		label: 'Is author',
		help: 'Is the user a author or not?',
	}
},
```




## range

#### label:

If set, a label will be generated using label property value as the content.
* Type: `String`
* Required: No

#### help:

If set, a help text will be generated using help property value as the content.
* Type: `String`
* Required: No

#### beforeIcon:

If set, a dashIcon component will be rendered before the slider with the icon equal to beforeIcon.
* Type: `String`
* Required: No

#### afterIcon:

If set, a dashIcon component will be rendered after the slider with the icon equal to afterIcon.
* Type: `String`
* Required: No

#### allowReset:

If set to `true`, a button to reset the the slider is rendered.
* Type: `Boolean`
* Required: No

#### value:

The current value of the range slider.
* Type: `Number`
* Required: Yes

#### onChange:

A function that receives the new value. If allowReset is true, when onChange is called without any parameter passed it should reset the value.
* Type: `function`
* Required: No

For more [read gutenberg readme](https://github.com/WordPress/gutenberg/tree/master/components/range-control).

**Example:**

```js
range: {
	type: 'string',
	field: {
		type: 'range',
		label: 'Columns',
		value: columns,
		onChange: onChange,
		min: 2,
		max: 10
	},
}
```



## url

#### value:

Value of url field.

- Type: `String`
- Required: No

#### onChange:

A function that receives the value of the new option that is being selected as input.

- Type: `function`
- Required: No

For more [read gutenberg readme](https://github.com/WordPress/gutenberg/tree/master/blocks/url-input).

**Example:**

```js
url: {
	type: 'string',
	field: {
		type: 'url',
	},
}
```



## select

#### label:

If set, a label will be generated using label property value as the content.
* Type: `String`
* Required: No

#### help:

If set, a help text will be generated using help property value as the content.
* Type: `String`
* Required: No

#### multiple:

If set, multiple values can be selected.
* Type: `Boolean`
* Required: No

#### options:

An array of objects containing the following properties:
* `label:` (string) The label to be shown to the user.
* `value:` (Object) The internal value used to choose the selected value. This is also the value passed to onChange when the option is selected.


* Type: `Array`
* Required: No

#### onChange:

A function that receives the value of the new option that is being selected as input. If multiple is true the value received is an array of the selected value. If multiple is false the value received is a single value with the new selected value.
* Type: `Function`
* Required: No

For more [read gutenberg readme](https://github.com/WordPress/gutenberg/tree/master/components/select-control).

**Example:**

```js
selectOption: {
	type: 'string',
	field: {
		type: 'select',
		label: 'Select Numbers',
		options: [
			{
				value: 'one',
				label: 'one',
			},
			{
				value: 'two',
				label: 'two',
			},
		],
	},
}
```



## image / video / audio

#### buttonText:

Upload button text.

- Type: `string`
- Required: No
- Default: null

#### imagePlaceholder:

Show image placeholder.

- Type: `bool`
- Required: No
- Default: false

#### removeButtonText:

Remove media button text. Remove button is visible only when `removeButtonText` is set.

- Type: `string`
- Required: No
- Default: null

#### multiple:

Whether to allow multiple selections or not.

- Type: `Boolean`
- Required: No
- Default: false

#### value:

Media ID (or media IDs if multiple is true) to be selected by default when opening the media library.

- Type: `Number|Array`
- Required: No

#### onSelect:

Callback called when the media modal is closed, the selected media are passed as an argument.

- Type: `Function`
- Required: No

#### render:

A callback invoked to render the Button opening the media library.

- Type: `Function`
- Required: No

For more [read gutenberg readme](https://github.com/WordPress/gutenberg/tree/master/blocks/media-upload).

**Example:**

```js
image: {
	type: 'object',
	field: {
		type: 'image',
		buttonText: __( 'Upload' ),
		imagePlaceholder: true,
		removeButtonText: __( 'Remove' ),
	},
},
```



## editor

#### value:

The source code to load into the code editor.

- Type: `string`
- Required: No

#### focus:

Whether or not the code editor should be focused.

- Type: `bool`
- Required: No
- Default: false

#### onFocus:

The function called when the editor is focused.

- Type: Function
- Required: No

#### onChange:

The function called when the user has modified the source code via the editor. It is passed the new value as an argument.

- Type: `Function`
- Required: No

For more [read gutenberg readme](https://github.com/WordPress/gutenberg/blob/master/components/code-editor/README.md).

**Example:**

```js
editorContent: {
	type: 'string',
	field: {
		type: 'editor',
	},
},
```



## date-time

#### label:

Field Label

- Type: `string`
- Required: No
- Default: 'Date'

#### currentDate:

The current date and time at initialization.

- Type: `string`
- Required: No

#### onChange:

The function called when a new date or time has been selected. It is passed the `currentDate` as an argument.

- Type: `Function`
- Required: No

#### locale:

The localization for the display of the date and time.

- Type:`string`
- Required: No

#### is12Hour:

Whether the current timezone is a 12 hour time.

- Type: `bool`
- Required: No

For more [read gutenberg readme](https://github.com/WordPress/gutenberg/blob/master/components/date-time/README.md).

**Example:**

```js
dateTime: {
	type: 'string',
	field: {
		type: 'date-time',
		position: 'inspector',
	},
},
```



## color

#### label:

The title of color control

- Type: `string`
- Required: No
- Default: 'Color'

#### value:

The value of color.

- Type: `string`
- Required: No

#### onChange:

The function called when a new color has been selected. It passes the new value as an argument.

- Type: `Function`
- Required: No

For more [read gutenberg readme](https://github.com/WordPress/gutenberg/tree/master/blocks/color-palette ).

**Example:**

```js
color: {
	type: 'string',
	field: {
		type: 'color',
		position: 'inspector',
	},
},
```



## switch

#### label:

Field Label

- Type: `string`
- Required: No

#### checked:

Checked attribute of checkbox. Changes the accessibility text to "On/Off".

- Type: `bool`
- Required: No

#### onChange:

The function called when switch toggles. It passes the new value as an argument.

- Type: `Function`
- Required: No

For more [read gutenberg readme](https://github.com/WordPress/gutenberg/tree/master/components/form-toggle ).

**Example:**

```js
switch: {
	type: 'string',
	field: {
		type: 'switch',
		label: __( 'Form Toggle' ),
		position: 'inspector',
	},
},
```



## textarea

#### value:

The current value of the textarea.

- Type: `string`
- Required: No

#### onChange:

A function that receives the new value of the textarea each time it changes.

- Type: `Function`
- Required: No

#### label:

If this property is added, a label will be generated using label property as the content.

- Type: `String`
- Required: No

#### help:

If set, a help text will be generated using help property as the content.

- Type: `String`
- Required: No

#### row:

The number of rows the textarea should contain. Defaults to four.

- Type: `String`
- Required: No
- Default: 4

For more read gutenberg [readme](https://github.com/WordPress/gutenberg/tree/master/components/textarea-control).

**Example:**

```js
textarea: {
	type: 'string',
	field: {
		type: 'textarea',
		label: __( 'Textarea' ),
		position: 'inspector',
	},
},
```



## email / number/ hidden / search / tel

Creates input fields with above types. You can pass key value pairs will be passed to the input. 

#### onChange:

A function that receives the new value of the input field each time it changes.

- Type: `Function`
- Required: No

#### label:

If this property is added, a label will be generated using label property value as the content.

- Type: `String`
- Required: No

#### help:

If set, a help text will be generated using help property as the content.

- Type: `String`
- Required: No

#### className:

CSS class name for the input field.

- Type: `String`
- Required: No

**Examples:**

```js
email: {
	type: 'string',
	field: {
		type: 'email',
		label: __( 'Email' ),
		position: 'inspector',
	},
},
hidden: {
	type: 'string',
	field: {
		type: 'hidden',
		position: 'inspector',
	},
},
number: {
	type: 'string',
	field: {
		type: 'number',
		label: __( 'Number' ),
		position: 'inspector',
	},
},
search: {
	type: 'string',
	field: {
		type: 'search',
		label: __( 'Search' ),
		position: 'inspector',
	},
},
tel: {
	type: 'string',
	field: {
		type: 'tel',
		label: __( 'Telephone' ),
		position: 'inspector',
	},
},
```





---

The plugin is currently just a proof of concept of the idea suggested by Daniel in his post [fields-middleware-for-gutenberg](https://danielbachhuber.com/2018/02/27/fields-middleware-for-gutenberg/)
