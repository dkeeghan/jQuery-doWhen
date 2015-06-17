# jQuery-doWhen
jQuery plugin to handle customisable actions (like show, hide, disable, click) based on changing form field values

## Getting started
At it's simplest just grab `jquery.dowhen.js` include it in your site and run `$(document).doWhen();`

```html
<script src="/path/to/libs/jquery.dowhen.js"></script>

<script>
	$(document).ready(function(){
		$(document).doWhen();
	});
</script>
```
In the HTML, you'll need two `data-` attributes:
* **`data-do-when`**<br/>The conditions to be used to determine when to call the action (in JSON).
* **`data-do-action`**<br/>The action to be called.

The following example will `show` the `<div>` when the `<select>` element with the ID `select-box` has the option selected with the value of `yes`.
```html
<div data-do-when='{ "select-box": ["yes"] }' data-do-action="show">
	Some content to show when the select box is equal to "yes"
</div>
```
**Note:** you'll need to either use single quotes for the attributes, or escape the inner double quotes as JSON is only valid using double quotes.

## Conditions
At it's most basic level the condition is a JSON object where the key is the `id` or `name` attribute of the form field to be looked at, and the value is an array of possible values that the form field can be.

### Basic conditions

```json
{ "select-box": ["yes"] }
```
**Above:** If the field with id `select-box` has the value of `yes`<br/><br/>

```json
{ "select-box": ["yes", "no"] }
```
**Above:** If the field with id `select-box` has the value of `yes` **OR** `no`<br/><br/>

### Checking multiple fields

You can also check multiple fields before the condition is successful:

```json
{ "select-box": ["yes"], "checkbox": ["item-1"] }
```
**Above:** If the field with id `select-box` has the value of `yes` **AND** the checkbox group with name `checkbox` has `item-1` checked.<br/><br/>

```json
{ "select-box": ["yes"] } || { "checkbox": ["item-1"] }
```
**Above:** If the field with id `select-box` has the value of `yes` **OR** the checkbox group with name `checkbox` has `item-1` checked.<br/><br/>

## Actions
Included by default are the following actions:

**`show`**<br/>Shows the element when the conditions are met. By default will hide the element.

**`hide`**<br/>Hides the element when the conditions are met. By default will show the element.

**`click`**<br/>Clicks the element when the conditions are met. Does nothing if not met.

**`disable`**<br/>Disables the element when the conditions are met. Re-enables the element when not met. If the element to be disabled is an `<option>` inside a `<select>` element, it will check and disable the entire `<select>` if there are no other options available to choose.

You can add your own custom actions by using the `$.doWhen.addAction()` method.

## Options
You can customise the `data-` attribute names used by the plugin, just in case you're already using something similar and you want it to read easier. For most users you should need to change this.

**`doWhenAttr`** (String)<br/>Change the `data-` attribute for the logic. Default: `'do-when'`

**`doActionAttr`** (String)<br/>Change the `data-` attribute for the action. Default: `'do-action'`

## Methods
Currently there is only one method:

### `$.doWhen.addAction(name, match, unmatch)`
Add a new custom action for use in your project with three inputs:

**`name`** (String)<br/>The name of the action. If you want to override an existing action, use the same name as one of the existing ones to override it.

**`match`** (`function($el, callback)`)<br/>Function to call on match of the conditions. Has two variables passed through. `$el` is the element, and `callback` is a function to be called on completion.

**`unmatch`** (`function($el, callback)`)<br/>Function to call on unmatch of the conditions. Has two variables passed through. `$el` is the element, and `callback` is a function to be called on completion.

## Events
A series of events are fired on update of the elements so you can listen for changes.

**`updated.doWhen`**<br/>Triggered from the element on update (match or unmatch)

**`matched.[action].doWhen`**<br/>Triggered from the action `[action]` on match. E.g. the `show` event will trigger the event `matched.show.doWhen`.

**`unmatched.[action].doWhen`**<br/>Triggered from the action `[action]` on match. E.g. the `show` event will trigger the event `unmatched.show.doWhen`.