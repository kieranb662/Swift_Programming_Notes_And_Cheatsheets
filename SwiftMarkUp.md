# Swift MarkUp 

  * [Basic Syntax](#basic-syntax)
  * [Some Delimeters](#some-delimeters)
  * [Generic Example](#generic-example)

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
