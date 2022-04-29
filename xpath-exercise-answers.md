# XPath exercises answers

## 1. Path expressions 

- Write an absolute path that finds all speech elements

`/TEI/text/body/div/div/sp`

- Write an absolute path that finds all 'role' attribute values in the cast list

`/TEI/text/front/div/castList/castItem/@type`

- Write a relative path that finds all speaker elements

`//speaker`

- Write an relative path that finds all who attributes

`//@who`

## 2. Axis expressions

- Write an axis expression that finds all sibling elements of second-level divs

`//div/div[self::* or following-sibling::div]`

- Write an axis expression that finds all parent nodes of stage elements

`//stage/parent::*`

- Write an axis expression that finds all speeches that come before or after a Hamlet speech.

`//sp[@who="Hamlet"]/following-sibling::sp[1] | preceding-sibling::sp[1]`

## 3. Predicates

- Find all speech elements for all speakers except Hamlet

`//sp[not(@who='Hamlet')]`
- Find all speech elements by Hamlet and Ophelia

`//sp[@who='Hamlet'] | //sp[@who='Ophelia']` or `//sp[@who=('Hamlet', 'Ophelia')]`

- Find the last line of each speech by Ophelia

`//sp[@who='Ophelia']/l[last()]`

## 4. Functions

- Write a function to count speakers

`count(//speaker)`

- Write a function to list only the distinct speakers (so a list of the speakers)

`distinct-values(//speaker)`

- Write a function to return all lines in speeches that contain the string ‘Hamlet’, (except speaker elements)

`//sp/l[contains(., 'Hamlet')]`

- Find the string length of each of Hamlet’s speeches.

`//sp[@who='Hamlet']/l ! string-length(.)`

- Write a function to return all first lines of speeches greater than 100 characters

`//l[1][string-length() gt 100]`

- Calculate the average character count of Hamlet’s speeches.

`avg(//sp[@who='Hamlet']/l ! string-length(.))`

- List the distinct values of each speaker (i.e. list of characters) in Act 1

`distinct-values(//body/div[1]//speaker)`

## XPath builder exercise

- Use the previous expression to build a list separated by commas

```
//body/div[1]//speaker
=> distinct-values()
=> sort()
=> string-join(', ')
```
 
- Write an XPath expression to list an alphabetised list of words spoken by Ophelia that came after ‘I’.

```
//sp[@who='Ophelia']/(l | ab)
[tokenize(.)[1] eq 'I']
/tokenize(.)[2]
=> distinct-values()
=> sort()
```
