# jQuery-doWhen
jQuery plugin to handle customisable actions (like show, hide, disable, click) based on changing form field values

## Getting started
At it's simplest just grab `jquery.dowhen.js` include it in your site and run `$('body').doWhen();`

```html
<script src="/path/to/libs/jquery.dowhen.js"></script>

<script>
	$(document).ready(function(){
		$('body').doWhen();
	});
</script>
```
In the HTML, you'll need two `data-` attributes:
* `data-do-when`: The logic to be used to determine when to call the action in a JSON object where the key is the `id` or `name` attribute of the form field(s) to be looked at.
* `data-do-action`: The action to be called.

*Note:* you'll need to either use single quotes for the attributes, or escape the inner double quotes as JSON is only valid using double quotes.

The following example will `show` the `<div>` when the `<select>` element with the ID `select-box` has the option selected with the value of `yes`.
```html
<div data-do-when='{ "select-box": ["yes"] }' data-do-action="show">
	Some content to show when the select box is equal to "yes"
</div>
```
## Actions
Included by default are the following actions:
* `show`: Shows the element when the conditions are met. By default will hide the element.
* `hide`: Hides the element when the conditions are met. By default will show the element.
* `click`: Clicks the element when the conditions are met. Does nothing if not met.
* `disable`: Disables the element when the conditions are met. Re-enables the element when not met. If the element to be disabled is an `<option>` inside a `<select>` element, it will check and disable the entire `<select>` if there are no other options available to choose.

You can add your own custom actions by using the `$.doWhen.addAction()` method.

## Options
You can customise the `data-` attribute names used by the plugin, just in case you're already using something similar and you want it to read easier. For most users you should need to change this.

### `doWhenAttr`
* *Type:* String 

Change the `data-` attribute for the logic. Default: `'do-when'`

### `doActionAttr`
* *Type:* String

Change the `data-` attribute for the action. Default: `'do-action'`

## Methods
Currently there is only one method:

### `$.doWhen.addAction(name, match, unmatch)`
Add a new custom action for use in your project with three inputs:

#### `name`
* *Type:* String

The name of the action. If you want to override an existing action, use the same name as one of the existing ones to override it.

#### `match`
* *Type:* `function($el, callback)`

Function to call on match of the conditions. Has two variables passed through. `$el` is the element, and `callback` is a function to be called on completion.

#### `unmatch`
* *Type:* `function($el, callback)`

Function to call on unmatch of the conditions. Has two variables passed through. `$el` is the element, and `callback` is a function to be called on completion.

## Events
A series of events are fired on update of the elements so you can listen for changes.

### `updated.doWhen`
Triggered from the element on update (match or unmatch)

### `matched.[name].doWhen`
Triggered from the action `[name]` on match. E.g. the `show` event will trigger the event `matched.show.doWhen`.

### `unmatched.[name].doWhen`
Triggered from the action `[name]` on match. E.g. the `show` event will trigger the event `unmatched.show.doWhen`.


## LICENSE (BSD-3-Clause)
Copyright (c) 2015, Damian Keeghan
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

* Redistributions of source code must retain the above copyright notice, this
  list of conditions and the following disclaimer.

* Redistributions in binary form must reproduce the above copyright notice,
  this list of conditions and the following disclaimer in the documentation
  and/or other materials provided with the distribution.

* Neither the name of jQuery-doWhen nor the names of its
  contributors may be used to endorse or promote products derived from
  this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE LIABLE
FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL
DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR
SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER
CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY,
OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
