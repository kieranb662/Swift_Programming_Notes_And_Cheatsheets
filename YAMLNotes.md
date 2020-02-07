# YAML 

* [Indentation](#indentation)
* [Numeric Values](#numeric-values)
* [Strings](#strings)
* [Nulls](#nulls)
* [Booleans](#booleans)
* [Arrays](#arrays)
* [Dictionaries](#dictionaries)
* [Anchors](#anchors)
* [References](#references)

YAML is a simple serialization language that is used by many as a format for configurations files.  YAML uses key-value pairs like JSON.    Comments are written by Prepending a `#` to the comment. 

## Indentation

All indentation must be in the form of spaces (**Not** tabs).

## Numeric Values 

Values that can be recognised come in the form of 
* Integers (decimal, hexidecimal , or octal)
* Floating point
* Scientific Notation (eg. 12.3015e+05)
* Infinity (eg.  .inf)
* Not a Number (.NAN)


## Strings

Strings do not need to be wrapped in double quotes unless you wish to have escaped sequences handled. 

Multiline strings can be converted to single lines by using the `>` character in the first line of the value 
````
bar: >
this is not a normal string it
spans more than
one line
see?
````
To keep the lines formatted as is use the `|` operator 
````
bar: |
this is not a normal string it
spans more than
one line
see?
````

## Nulls

Use either `~` or the unquoted word `null`

## Booleans

True can be written in the following ways: 
* True 
* On 
* Yes 

False can be written in the following ways 
* False 
* Off
* No

## Arrays

Arrays in YAML can be represented in either brackets `[...]` or in the multiline format 
````
items:
  - 1 
  - 2 
  - 3
  - 4 
  - 5 
names:
  - "one"
  - "two"
  - "three"
  - "four"
  ````
  
## Dictionaries
  
Similar to arrays, dictionaries can come in a single line format `{...}` or in the multiline form.
  ````
  foo:
  bar:
    - bar
    - rab
    - plop
    
````

## Anchors

If values are to be referenced or used multiple times, anchors can be used to reduce copy/pasting long entries multiple times.  Here is an example from the spec website link. 
```
hr:
  - Mark McGwire
  # Following node labeled SS
  - &SS Sammy Sosa
rbi:
  - *SS # Subsequent occurrence
  - Ken Griffey
```

## References
* YAML Spec - https://yaml.org/spec/1.2/spec.html
* Info on the `<<` - https://stackoverflow.com/questions/41063361/what-is-the-double-left-arrow-syntax-in-yaml-called-and-wheres-it-specced

