# CheatSheets and Notes

* Swift Markup
* YAML 
* Moustache 
* Shell


# Swift MarkUp 

Not everything is here, I never really found a use for all of it so I just kept the stuff I used frequently.

## Basic Syntax

| Style                 | Syntax                          | Rendered                       |
|-----------------------|---------------------------------|--------------------------------|
| Single Row Comment    | /// Example                     | Example                        |
| Block Comment         | /** <br>Example<br>*/           | Example                        |
| Header(H1)            | \# example                      |                                |
| Header(H2)            | \#\# example                    |                                |
| Italicized            | \*example\*                     | *example*                      |
| Bold                  | \*\*example\*\*                 | **example**                    |
| Unordered List        | \* example                      |                                |
| Ordered List          | 1. example                      |                                |
| Inline Code           | \`var example\`                 | `var example`                  |
| Multi-Line Code Block | \`\`\`<br>var example<br>\`\`\` | ```   var example   ``` |

## Some Delimeters

|            |               |              |
|------------|---------------|--------------|
| Attention  | Invariant     | Since        |
| Author     | Note          | Throws       |
| Authors    | Parameter     | To Do        |
| Bug        | Parameters    | Version      |
| Copyright  | Postcondition | Warning      |
| Complexity | Returns       | Precondition |
| Date       | Requires      | Remark       |
| Important  | See Also      | Images       |


## Generic Example

``` Swift
/**
# Important Function

Example description of a function 
- parameters:
  - first: Description of *first*
  - second: Description of *second*
  
- returns: *third* number 

*/
```

# YAML 

YAML is a simple serialization language that is used by many as a format for configurations files.  YAML uses key-value pairs like JSON.    Comments are written by Prepending a `#` to the comment. 

**Indentation** 

All indentation must be in the form of spaces (**Not** tabs).

**Numeric Values** 

Values that can be recognised come in the form of 
* Integers (decimal, hexidecimal , or octal)
* Floating point
* Scientific Notation (eg. 12.3015e+05)
* Infinity (eg.  .inf)
* Not a Number (.NAN)


**Strings** 

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

**Nulls**

Use either `~` or the unquoted word `null`

**Booleans**

True can be written in the following ways: 
* True 
* On 
* Yes 

False can be written in the following ways 
* False 
* Off
* No

**Arrays** 

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
  
**Dictionaries** 
  
Similar to arrays, dictionaries can come in a single line format `{...}` or in the multiline form.
  ````
  foo:
  bar:
    - bar
    - rab
    - plop
    
````

**Anchors**

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

**References** 
* YAML Spec - https://yaml.org/spec/1.2/spec.html
* Info on the `<<` - https://stackoverflow.com/questions/41063361/what-is-the-double-left-arrow-syntax-in-yaml-called-and-wheres-it-specced


# .moustache

The mustache file format is used to create "Logic-less templates" for various file types. There are no if statements, else statements, or for loops. The only component found within them is the **tags** . 

**Variables** 

`{{variable}}` is a tag whose key(variable) will be searched for in the current context. 

for unescaped HTML use `{{{variable}}}` or  `{{& variable}}`

**Sections** 

A section begins with a `{{#variable}}` and ends with a `{{/variable}}`.  Behavior of the section is determined by the value of the key. 

* For false or empty values - The section is not rendered. 
* For non-empty lists - the value in the section will be rendered once for each item in the list. 
* lambdas - if the section value is a callable function, should handle its own creation of the block. 
* Non-False values - renders the block with the value once 

**Inverted Sections**

A section begins with a `{{^variable}}` and ends with a `{{/variable}}`.  Behavior of the section is determined by the value of the key. In this case text will be rendered if the value of the key doesnt exist, is false or is an empty list. 

**Comments** 

Written in the form `{{! variable}}`.  These values will never be rendered. 

**Partials** 

Written in the form `{{> variable}}`. Used for referencing other mustache files to be nested within the current file.


**References** 

* Mustache Manual - https://mustache.github.io/mustache.5.html
