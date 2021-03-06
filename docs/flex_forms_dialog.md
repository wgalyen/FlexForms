FlexForms.Dialog Class:
=======================

The FlexForms.Dialog Javascript class adds a movable, resizeable, modal dialog to FlexForms. FlexForms.Dialog is a useful layer to display a FlexForms form in a dialog.

FlexForms is a powerful HTML forms generator/builder class to output HTML forms from Javascript using a natural JSON-style arrays approach.

Example usage:

```html
<script type="text/javascript" src="flexforms/flex_forms.js"></script>
<script type="text/javascript" src="flexforms/flex_forms_dialog.js"></script>

<script type="text/javascript">
(function() {
	var options = {
		title: 'Dialog Title',

		content: {
			fields: [
				'startrow',
				{
					title: 'First Name',
					width: '19em',
					type: 'text',
					name: 'first_name',
					default: 'Joe'
				},
				{
					title: 'Last Name',
					width: '18em',
					type: 'text',
					name: 'last_name',
					default: 'Smith'
				},
				'endrow',
				{
					title: 'Test Multiselect',
					width: '38em',
					type: 'select',
					multiple: true,
					name: 'test_select',
					options: [
						{ name: 'Test 1', value: 'Test 1' },
						{ name: 'Test 2', value: 'Test 2' },
						{ name: 'Test 3', value: 'Test 3' },
					],
					default: { 'Test 1': true, 'Test 3': true }
				}
			],
			submit: ['OK', 'Cancel'],
			submitname: 'test_submit'
		},

		onsubmit: function(formvars, formnode, e) {
            console.log(formvars);

			this.Destroy();
		},

		onclose: function() {
            console.log('Close');

			this.Destroy();
		}
	};

	var dlg = FlexForms.Dialog(document.body, options);
})();
</script>
```

FlexForms.Dialog(parentElem, options)
-------------------------------------

Category: Constructor

Parameters:

* parentElem - a DOM node to append the root of the dialog to (document.body is recommended).
* options - An object containing options to use to construct the dialog.

Returns: A Javascript function hierarchy.

This function sets up a new FlexForms.Dialog instance.

The options object can contain the following:

* Modal - A boolean indicating whether or not the dialog will be modal (Default is true).
* backgroundCloses - A boolean indicating whether or not clicking off the dialog will close the dialog (Default is false).
* move - A boolean indicating whether or not the dialog can be resized by draging the edges (Default is true).
* title - A string containing a  title to use for th etitle bar of the dialog (Default is '').
* content - An object containing FlexForms.Generate() options (Default is an empty object).
* errors - An object containing FlexForms.Generate() errors (Default is an empty object).
* request - An object containing FlexForms.Generate() request variables (Default is an empty object).
* onPosition(elem) - An optional callback that is invoked whenever the position or size of the dialog has changed (Default is null).
    * elem - The main DOM element of the dialog.
* onSubmit(formData, formElem, e) - An optional callback that is invoked when a form submission happens (Default is null).
    * formData - An object containing all the field name/value paris of submitted data including the button that was pressed.
    * formElem - A DOM element pointing to the form.
    * e - An event object containing the submit event.
* onClose() - An optional callback that is invoked when the dialog should close (Default is null).
* onDestroy() - An optional callback that is invoked when the dialog instance is destroyed (Default is an empty object).

FlexForms.Dialog.settings
-------------------------

Category: Settings

The `settings` object contains the settings for the instance. Changing the setting after creating the instance will have little to no effect.

FlexForms.Dialog.addEventListener(eventName, callback)
------------------------------------------------------

Category: Events

Parameters:

* eventName - A string containing a name of a FlexForms.Dialog event to listen to.
* callback - A function to call when the event fires.

Returns: Nothing

This function presents a familiar function for registering for custom events emitted by FlexForms.Dialog.

Known events:

* position - Dispatched when the dialog position or size changes.
* submit - Dispatched when a dialog submit button is pressed or the form is submitted.
* close - Dispatched when the dialog should close.
* destroy - Dispatched when the Destroy() function is called.

Most of these events have equivalents in the settings object and associated callbacks will automatically be registered as event listeners during initialization.

FlexForms.Dialog.removeEventListener(eventName, callback)
---------------------------------------------------------

Category : Events

Parameters:

* eventName - A string containing a name of a FlexForms.Dialog event to stop listening to.
* callback - A function containing a registered callback to remove.

Returns: Nothing

This function presents a familiar function for unregistering form custom events emitted by FlexForms.Dialog.

FlexForms.Dialog.hasEventListener(eventName)
--------------------------------------------

Category: Events

Parameters:

* eventName - A string containing a name of a FlexForms.Dialog event to check.

Returns: A boolean of true if there are event listeners for the specified, false otherwise.

This function checks for the existence of an event and whether or not there are any listeners registered for the event.

FlexForms.Dialog.UpdateContent()
--------------------------------

Category: Forms

Parameters: None.

Returns: Nothing.

This function regenerates the FlexForms form and updates the dialog in-place. Useful for emitting error messages after validating submitted information.

FlexForms.Dialog.UpdateSizes()
------------------------------

Category: Miscellaneous

Parameters: None

Returns: Nothing.

This function adjusts the dialog and recalculates the internal position and size tracking information. Used by SnapToScreen() and CenterDialog().

FlexForms.Dialog.SnapToScreen()
-------------------------------

Category: Position and Size

Parameters: None.

Returns: Nothing.

This function snaps the dialog so that it fits on the screen. Generally only called if the dialog has been moved or resized.

FlexForms.Dialog.CenterDialog()
-------------------------------

Category: Position and Size

Parameters: None

Returns:  Nothing.

This function moves the dialog to the center of the screen unless it has been manually moved or resized.

FlexForms.Dialog.Close()
------------------------

Category:  Closing

Parameters:  None.

Returns:  Nothing.

This function calls registered close callbacks for the dialog.

FlexForms.Dialog.Destroy()
--------------------------

Category:  Destructor

Parameters:  None.

Returns:  Nothing.

This function cleans up the DOM and destroys the instance.  Calling other functions after this function will result in an error or undefined behavior.

