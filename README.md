MooTools-DatePicker
===================

MooTools DatePicker is a nice modular and themable DatePicker. It has many features and options, such as
year, month, day or timepicker only modes, min and max dates, Localization and a lot more.

This Plugin makes use of MooTools' Locale and Date plugins in MooTools More, to provide a localized
datepicker, as well as easy formatting and parsing Dates.

This DatePicker is a fork of the original [MonkeyPhysics DatePicker](http://www.monkeyphysics.com/mootools/script/2/datepicker),
and has improved a lot since then. Though it should be (almost) backward compatible.

![Screenshot](https://github.com/arian/mootools-datepicker/raw/master/screenshot.png)

As of version 1.60 the datepicker will only work with MooTools 1.3.

How to use
----------

Below you will find a description and some docs how you can use the datepicker.
If you find any weird things, please create a ticket at github or fork and fix it!

The DatePicker consists out of three layers, a Picker class, which can be used to create  any form of Picker, a Picker.Attach class,
which handles stuff like attaching the Picker to a input or anchor element. Finally there is the DatePicker class, which you'll probably
use. Every option of the Picker or Picker.Attach classes can be used in the DatePicker class.

Basic Example
-------------

First you need to include the following html tags:

	#HTML
	<script src="../Source/Locale.en-US.DatePicker.js" type="text/javascript"></script>
	<script src="../Source/Picker.js" type="text/javascript"></script>
	<script src="../Source/Picker.Attach.js" type="text/javascript"></script>
	<script src="../Source/Picker.Date.js" type="text/javascript"></script>

	<link href="../Source/datepicker_dashboard/datepicker_dashboard.css" rel="stylesheet">

Then you can simply use, for example:

	#JS
	new Picker.Date($$('input'), {
		timePicker: true,
		positionOffset: {x: 5, y: 0},
		pickerClass: 'datepicker_dashboard',
		useFadeInOut: !Browser.ie
	});


### Theming:

Theming is done with CSS files, there are four themes available, which you can find in the Source folder.

Just include the CSS file and set the `pickerClass` option.


### Localization

The DatePicker uses the MooTools More Date Class, which already includes many localized strings.
For some specific strings DatePicker has its own localizations, which you can find in the Locale.__-__.DatePicker.js files.
Just include the file in your page with a script tag to use the translations.

Currently the following languages are supported

- en-US
- nl-NL
- cs-CZ
- ru-RU

You can set the current language with:

	#JS
	Locale.use('nl-NL');


Class: DatePicker
-----------------

### Syntax

	#JS
	var dp = new DatePicker([element, options]);

### Arguments

1. element: (*element*, *string*, *array*) The element(s) to attach the datepicker to
2. options: (*object*, optional) The options object

### Options:

All the options of the Picker and Picker.Attach classes, and:

- minDate: (*Date instance*, *string*, defaults to `null`) Minimum date allowed to pick. Blocks anything before.
- maxDate: (*Date instance*, *string*, defaults to `null`) Maximum date allowed to pick. Blocks anything after.
- format: (*string*, defaults to the default localized format) The format to output into the input field. Uses [Date.format](http://mootools.net/docs/more/Types/Date#Date:format)
- timePicker: (*boolean*, defaults to 1 `false`) Enable/disable timepicker functionality. Hours/Minutes values can be changed using the scrollwheel.
- timeWheelStep: (*number*, defaults to `1`) The number of minutes the minutes field will change in the timepicker when using the scrollwheel, for example 5, 10, 15. The value will always be k * timeWheelStep.
- yearPicker: (*boolean*, defaults to `true`) Enable/disable yearpicker functionality. Makes it much easier to change years.
- yearPerPage: (*number*, defaults to `20`) Amount of years to show in the year-picking view. Be aware that this may affect your layout.
- startView: (*string*, defaults to `days`) The view that will be showed when the picker opens. The options are `time`, `days`, `months` and `years`
- pickOnly: (*string*, defaults to `false`) If you just want to pick a year, month, day or time. The options are `time`, `days`, `months` and `years`
- canAlwaysGoUp: (*array*, defaults to `['months', 'days']`) The views where you can click the title to go up. The options are `time`, `days`, `months` and `years`

### Events:

- onSelect: Will fire when the user has selected a date

#### signature

	#JS
	onSelect(date)

#### arguments

1. date - A Date object. You could use [Date.format](http://mootools.net/docs/more/Types/Date#Date:format) to format it into a string. For example to set it into a hidden field which will be sent to the server.


### Examples

	#JS
	new DatePicker('inputField', {
		timePicker: true,
		pickerClass: 'datepicker_jqui',
		onSelect: function(date){
			myHiddenField.set('value', date.format('%s');
		}
	});


Class: Picker.Attach
--------------------

Picker.Attach handles all the links from elements to the Picker. It handles the onfocus events of input elements etc.
The Class itself is not very useful on its own, but it is useful to extend this Class.
This class adds a outerclick as well to close the Picker if you click outside the picker.

#### Syntax:

	#JS
	new Picker.Attach(attachTo, options);

#### Options:

- toggle: (*element*, *string*, *array*) A collection of elements which will toggle the picker when such a link is clicked.


### Picker.Attach Method: attach

This will attach links and input elements to the picker

#### Syntax

	#JS
	myPicker.attach(attachTo);

#### Arguments

1. attachTo: (*element*, *string*, *array*) The elements or element to attach to the Picker. Can be a input element for onfocus events or other elements for click events.


### Picker.Attach Method: detach

This will detach links and input elements from the picker

#### Syntax

	#JS
	myPicker.detach(detach);

#### Arguments

1. detach: (*element*, *string*, *array*) The elements or element to detach from the Picker. Can be a input element for onfocus events or other elements for click events.


Class: Picker
-------------

This is a generic Picker Class, which is used for the basic things, like positioning, Fx, open, close, stuff like that.

#### Syntax:

	#JS
	new Picker(options);

#### Options:

- pickerClass: (*string*, defaults to `datepicker`) CSS class for the main datepicker container element.
- inject: (*element*, defaults to `document.body`) This is where the Picker element will be injected to.
- anitmationDuration: (*number*, defaults to `400`) Duration of the slide/fade animations in milliseconds.
- useFadeInOut: (*boolean*, defaults to `true`) Whether to fade-in/out the datepicker popup. You might want to set this to `false` in IE.
- positionOffset: (*object*, defaults to `{x: 0, y: 0}`) Allows you to tweak the position at which the datepicker appears, relative to the input element. Formatted as an object with x and y properties. Values can be negative.
- pickerPosition: (*string*, defaults to `bottom`) If the picker is positioned relative to an element, you can choose to position it top, bottom, left or right.
- draggable: (*boolean*, defaults to `true`) Will make the picker draggable, if Drag from MooTools More is included.

#### Events:

- open - triggered when the Picker will open (before the fx)
- close - triggered after the Picker is will get closed (before the fx)
- show - triggered when the Picker is shown
- hide - triggered when the Picker is hidden



### Picker Method: show

A method to show the Picker manually, with a Fx.

#### Syntax

	#JS
	dp.show()

### Picker Method: close

Closes the Picker with a Fx.

#### Syntax

	#JS
	dp.close();


### Picker Method: toggle

Toggles the Picker with a Fx.

#### Syntax

	#JS
	picker.toggle();

### Picker Method: show

Opens the Picker directly.

#### Syntax

	#JS
	dp.show();


### Picker Method: hide

Hides the Picker directly.

#### Syntax

	#JS
	dp.hide();


### Picker Method: destroy

Destroys the Picker

	#JS
	picker.destroy();


### Picker Method: position

Positions the Picker.

#### Syntax:

	#JS
	picker.position(x, y);
	// or
	picker.position(myElement, where);

#### Arguments

1. x: (*number*) Number of pixels from the left
2. y: (*number*) Number of pixels from the top

Or

1. myElement - (*element*) A element the Picker should be positioned relative to.
2. where - (*string*, optional) Position the Picker `left` or `right` to the element.


### Picker Method: setContent

Set the content of the Picker, either elements or text.

#### Syntax:

	#JS
	picker.setContent(element, fx);

#### Arguments:

1. element: (*element*, *string*) Set the content of the Picker with this value
2. fx: (*string*, optional) Set the content of the picker, and apply it with this Fx. Options: 'fade', 'right', 'left'


### Picker Method: setTitle

Sets the Picker title text.

	#JS
	picker.setTitle(text);

#### Arguments:

1. text: (*string*) The text which will be set into the title.



