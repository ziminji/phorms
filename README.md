# Changes in this branch

## tf198's changes
### Functional Changes:
* Changed how values passed via *$data* parameter are handled so there is a symmetric relationship between it and the validated output of
Phorm::cleaned\_data().  Before you couldn't display a form for stored data because certain fields like *Phorm\_Field\_Date* were populated
by one type (string) and returned another (unix timestamp).  All such fields should now provide an *export\_value($value)* method that performs
the inverse of *import\_value($value)*.

## petsagouris's changes
### Functional Changes:
* Removed client side validation to keep this library focused on PHP (not javascript)
* Added Alpha/Alphanumeric field type
* Added OptionGroup (multi-select checkbox) field type

### Non-Functional Changes:
* Made sure the examples (in the examples folder) were working as expected and that the code was clean.
* Note that the original branch developer has been contacted but has not responded -- this branch should probably be considered the most active.

## jordanlev's changes
### Functional Changes:
* Changed name of Phorm\_Field\_Numeric to Phorm\_Field\_Integer because that's what it is (numeric is misleading because php's is\_numeric() function checks for any kind of number, not just integers).
* Added $size parameter to Decimal and Integer field types instead of hard-coding "20".
* Simplified built-in 'required' validation (just add 'required' to any field's validation array) [Implementation Details: I removed the "Validation.class.php" file because it made no sense, and replaced it with a simple built-in function that is automatically called when is_valid() is called if the validation array contains 'required'].
* Changed default form method from 'get' to 'post' in the Phorm\_Phorm constuctor ('post' is a more common use case so it should be the default)
* Added a display\_errors() function that can be called on your phorm object to output a list of all field errors -- useful if you want to display all errors at the top of the page instead of inline with each feild.
* Added a new public fields() function to Phorm\_Phorm class so all field objects can be retrieved and looped through.
* Text and Integer fields now set HTML maxlength attribute based on $max\_length param (in addition to existing server-side validation check).
* Bugfix: The is\_valid() function in Field.class.php now works with instance callbacks as well as function names, to match documented behaviour.

### Non-Functional Changes:
* Added new designed\_form.php example to demonstrate how to use the class in your own templated / designed HTML form (as opposed to an auto-generated table), and to show off the new display\_errors() and fields() functions.
* Removed getIterator() function in Phorm/Phorm.class.php becaue it wasn't doing anything (class doesn't implement IteratorAggregate)
* Removed leftover debugging call to var\_dump() in Phorm/Field/Email.class.php
* Cleaned up some function comments in Phorm/Field.class.php
* Removed docs/ directory because it was autogenerated before I made all of these changes, so it was out of date (and I haven't re-generated it with phpDocumentor yet).
* Added constant for target directory to the file\_drop.php example
