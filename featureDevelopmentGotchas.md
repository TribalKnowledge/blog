# Edge Case Spidey Sense Tips and Tricks - Things to keep in mind for code development/reviews:
(aka this is the kind of shit that has bitten us in the past)

## Future proof?
Are you building in convention instead of design? How easy would it be for an unfamiliar dev to use your code improperly?

## Complete logic
Are there unaccounted for logical branches? Wherever there is an if, consider the else
 Use exhaustive switch cases, always.
 DO NOT PUT IN EMPTY CASES OR SWALLOW ERRORS - log at a minimum
 Kotlin specific - If we do the work inside of a .?let{} then what happens if the variable IS null?

## Persistent Data
Do the changes affect the schema of any persistent data? A migration is necessary.
Do the changes affect the state of any persistent data? DB values, shared prefs, files, the external settings in the device?
 Consider the possible states that an existing system could already have/be in. Is a migration necessary?

## Dependent Functionality
How will your changes affect any consuming code?
Have code changes affected the possible return types? Nullability in Java affecting Kotlin

## probably not applicable to the random reader, but makes sense to our projects:
Dynamic abilities needing static code/assets. Don't cross the dynamic/static barrier if possible. Once you go dynamic you can’t go back.
