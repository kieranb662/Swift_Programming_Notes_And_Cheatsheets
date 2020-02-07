# .moustache

* [Variables](#variables)
* [Sections](#sections)
* [Inverted Sections](#inverted-sections)
* [Comments](#comments)
* [Partials](#partials)
* [References](#references-1)

The mustache file format is used to create "Logic-less templates" for various file types. There are no if statements, else statements, or for loops. The only component found within them is the **tags** . 

## Variables

`{{variable}}` is a tag whose key(variable) will be searched for in the current context. 

for unescaped HTML use `{{{variable}}}` or  `{{& variable}}`

## Sections 

A section begins with a `{{#variable}}` and ends with a `{{/variable}}`.  Behavior of the section is determined by the value of the key. 

* For false or empty values - The section is not rendered. 
* For non-empty lists - the value in the section will be rendered once for each item in the list. 
* lambdas - if the section value is a callable function, should handle its own creation of the block. 
* Non-False values - renders the block with the value once 

## Inverted Sections

A section begins with a `{{^variable}}` and ends with a `{{/variable}}`.  Behavior of the section is determined by the value of the key. In this case text will be rendered if the value of the key doesnt exist, is false or is an empty list. 

## Comments 

Written in the form `{{! variable}}`.  These values will never be rendered. 

## Partials 

Written in the form `{{> variable}}`. Used for referencing other mustache files to be nested within the current file.


## References

* Mustache Manual - https://mustache.github.io/mustache.5.html
