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
* [interesting pseudo-class link](https://developer.mozilla.org/en-US/docs/Web/CSS/:is)



### `(an + b)` psuedo-class selector formula
* `an+b`: selects any html element targeted by the selector if it is the (an+b)th child element in its parent HTML element
    - n: any number (0, 1, 2, 3...)
    - a: integer (default = 1)
    - b: integer (default = 0)
    - EX] `p:nth-child(n)` = `p:nth-child(1n+0)`
        - this will highlight every paragraph since it evaluated the `an+b` for EACH child
        - when you use `n`, it iterates through every child element and replaces the index that the child element is located in the `n` position
        - the outcome is the child it will style

            (1n+0) = 1 * **0** + 0 == 0 --> ignore since there are no "0" elements in the DOM tree

            (1n+0) = 1 * **1** + 0 == 1 --> styles the first element

            (1n+0) = 1 * **2** + 0 == 2 --> styles the second elemenet

            *...and so on*

            - remember, `(1n+0)` is the same as just using `n`, this is just for illustrative purposes
    - EX] `p:nth-child(2n)` == `p:nth-child(even)`

        (2n+0) = 2 * **0** + 0 == 0 --> ignore since there are no "0" elements in the DOM tree

        (2n+0) = 2 * **1** + 0 == 2 --> styles the second element

        (2n+0) = 2 * **2** + 0 == 4 --> styles the fourth element

    - EX] `p:nth-child(2n+1)` == `p:nth-child(odd)`

        (2n+1) = 2 * **0** + 1 == 1 --> styles the first element

        (2n+1) = 2 * **1** + 1 == 3 --> styles the third element

        (2n+1) = 2 * **2** + 1 == 5 --> styles the fifth element

    - **takeaways**: if you want to style multiples of a dom tree, just manipulate the `n`. because remember, `b` is defaulted to 0
    - So, for example, if you wanted multiples of five use `(5n)`

        (5n+0) = 5 * **0** + 0 == 0 --> ignore since there are no "0" elements in the DOM tree

        (5n+0) = 5 * **1** + 0 == 5 --> styles the fifth element

        (5n+0) = 5 * **2** + 0 == 10 --> styles the tenth element

        (5n+0) = 5 * **3** + 0 == 15 --> styles the fifthteenth element
    - **takeaways**: if you want to style multiples of a dom tree STARTING AT A POSITION, use the `b`
        - So, `(3n+2)` reads "select the multiples of three STARTING AT POSITION 2"
    - [Great YouTube video on the topic](https://www.youtube.com/watch?v=4NsJtaaC0qI)
* [`nth-of-child` vs. `nth-of-type`](https://css-tricks.com/the-difference-between-nth-child-and-nth-of-type/)
    - `nth-of-child(2)` means if it is the second child of its parent
    - `nth-of-type(2)` means select the second paragraph, REGARDLESS of if it is actually the second child of its parent
    
### Pseudo-elements
* Preceeded by two colons and can be added to the end of selectors to select a certain *part* of an element

## Combinators

* [Child vs descendent](http://www.peachpit.com/articles/article.aspx?p=1413883&seqNum=10)
* [css-tricks child selector](https://css-tricks.com/almanac/selectors/c/child/)
* [Stackoverflow child seelctor](https://stackoverflow.com/questions/33442967/difference-between-child-and-descendant-combinator-selectors)