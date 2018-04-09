# Forms

## Validation

Data validation should be done both front-end (for user convenience) and back-end (to ensure only valid data enters the system). Do not rely on front-end validation alone, client
requests can easily be forged.

1. Disruption: validation should not disrupt input. Typically, validation should occur at soonest when the user leaves a field, at the latest when they attempt an action that sends the
data elsewhere or hides the input field.
1. Communication: when validation fails a message should be displayed that clearly communicates the constraints. Ideally, the message should indicate which specific constraing failed.
	1. e.g. ✅ "Please enter only alphanumeric characters"
	1. e.g. ✅ "Please enter a value greater than 10"
	1. e.g. ❌ "Please enter a valid value" (this does not communicate what is invalid about the value)

## Formatting

Data formatting should always be clearly communicated to the user - this means that it should be done in the front-end, while the data is visible.

1. Disruption: formatting should not disrupt input. Inserting information ahead of where a user is typing is disruptive. Inserting information behind where a user is typing can also be
disruptive and should be done with care. Formatting is ideally done after a field loses focus; with care it can sometimes be done as a user types.
1. Communication: the desired format should be clearly displayed. Other formats in common use should be accepted while typing, but formatted to the desired format.

## Applying these guidelines to some common field types

### Date

Date and time values should use rich widgets that assist in selecting a value (`input type=[date|datetime-local|month|time|week]`). On platforms that don't support these (Internet Explorer), a 3rd-party widget should be used if possible. If not, then a text input with appropriate formatting and validation can be used.

#### Formatting

The date format should conform to the user's locale.

* US: MM-DD-YYYY
* The sane world: YYYY-MM-DD

The field should be somewhat flexible in the input it accepts: numbers, dashes, and forward slash.

* 10/10/2010
* 10-10-2010

Behavior:

* If only numbers are entered, add dashes in real-time BEHIND the user's typing
* If slashes are entered, replace with dashes BEHIND the user's typing

#### Validation

Minimum and maximum constraints (`min/max` attributes) should be supported. If validation fails the reason for failure should clearly be communicated for each case:

* The date is required but no value was entered
* The entered value is not a valid date
* The entered value is below the minimum acceptable value
* The entered value is above the maximum acceptable value

### Phone number

*NOTE:* This section currently only describes US phone numbers.

#### Formatting

XXX-XXX-XXXX

The field should accept input of: numbers, dashes, periods, parentheses, and spaces.

* 555-434-6000
* 555.434.6000
* (555) 434-6000

Behavior:

* If only numbers are entered, add dashes in real-time BEHIND the user's typing
* If periods are entered (in lieu of dashes), replace with dashes in real-time BEHIND the user's typing
* If parentheses or spaces are entered, delete AFTER typing is complete (and insert dashes where appropriate)

### Social Security Number

#### Formatting

XXX-XX-XXXX

The field should accept input of: numbers and dashes

* If only numbers are entered, add dashes in real-time BEHIND the user's typing
