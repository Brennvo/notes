# CSS Notes

* CSS declaration = property + value
    - property: `background-color`, `background`, etc.
    - value: 'red', '10px`, etc.
* Ruleset (AKA rule) = CSS declaration + declaration block
    - declaration block example
        ```css
        p {
            color: red;
            font-style: bold;
        }
        ```
* CSS shortcut order with four values --> ANALOG CLOCK
    - TOP, RIGHT, BOTTOM LEFT
* CSS shortcut order with two values
    - TOP/BOTOM, LEFT/RIGHT

## Attribute Selectors
* Value attribute selectors
    - `[attr]`
    - `[attr=val]`: only if the attribute has a value of `val`
    - `[attr~=val]`: if the attribute's value contains `val` somewhere in it
* Substring value attribute selectors
    - substring in this context is this: "cat" is a substring to "caterpillar"
    - `[attr^=val]` *and* `[attr|=val]` attribute must **START** with `val`
    - `[attr$=val]` attribute must **END** with `val`
    - `[attr*=val]` attribute must **CONTAIN** `val` in it

## Pseudo-classes and pseudo-elements
* These do *not* select elements, but rather, **parts** of an element or elements in certain contexts
* Pseudo-class: keyword added to the end of a selector preceded by a colon

    ![pseudo-classes](https://i.imgur.com/s7ui2kh.png)

* `:nth-child(n)`, where `n` can be a number, keyowrd, or mathematical formula
    `p:nth-child(1)` selec tthe first paragraph of its parent
    `p:nth-child(odd)` select the odd children paragraphs
* `an+b`: selects any html element targeted by the selector if it is the (an+b)th child element in its parent HTML element
    - n: any number (0, 1, 2, 3...)
    - a: integer (default = 1)
    - b: integer (default = 0)
    - EX] `p:nth-child(n)` = `p:nth-child(1n+0)`
        - this will highlight every paragraph since it evaluated the `an+b` for EACH child
        - when you use `n`, it iterates through every child element and replaces the index that the child element is located in the `n` position
            (1n+0) = 1 * **0** + 0 == 0
            (1n+0) = 1 * **1** + 0 == 1
            (1n+0) = 1 * **2** + 0 == 2
            *...and so on*
            - remember, `(1n+0)` is the same as just using `n`, this is just for illustrative purposes