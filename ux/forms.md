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
