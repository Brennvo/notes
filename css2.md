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
* `:only-of-type` can be tricky
    - if you do not add a tag before `:`, then it will match ANY tag that is the "only type" of it's parent
    - however, adding a tag will only target the "only type" of that tag
* [Codepen of `:only-of-type`](https://codepen.io/Hankis/pen/exLYvq)
        
    > you can think of div :only-of-type as being div *:only-of-type

    > if the document is like a tree, :only-of-type is going to target each tag that is the only one of its type on each 'level' of that tree. So with div *:only-of-type you're targeting any tag that's unique in its type among its siblings that's inside a <div> tag

    > that red anchor tag inside the <li>, inside the <ul> is the only <a> tag among its sibling elements



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
* [Stackoverflow descendent and appending class name example](https://stackoverflow.com/questions/16093883/p-classname-or-classname-p-any-difference)
* Using the adjacent sibling combinator
* `A + B`, where any element matching B that is the next sibling of an element matching A
    - Start with an example
        ```html
        <h3>Heading</h3>
        <h2>Random H2</h2>  // IT LOOKS HERE, SEES IT ISN'T A &lt;p&gt;, SO IT MOVES ON
        <p>Some stuff in a paragraph</p> // NOT RED
        <p>Some stuff in a paragraph</p>
        <p>Some stuff in a paragraph</p>
        <h3>Another heading</h3>
        <p>Some stuff in a paragraph</p>    // RED
        <p>Some stuff in a paragraph</p>
        <p>Some stuff in a paragraph</p>
        ```
        ```css
        h3 + p {
            color: red;
        }
        ```
    - Notice how this selector only deals with the *next* siling
* To target ALL siblings, you use the `~`
    - This would've also targeted that `<p>` tag
    ```css
    h3 ~ p {
        color: red;
    }
    ```
* Question, why do we get two red lines here?
    ```css
    p + p {
        color: red;
    }
    ```
    - Let's walk through the HTML
    ```html
        <h3>Heading</h3>
        <h2>Random H2</h2>
        <p>Some stuff in a paragraph</p> // Element that matches B, so go to next sibling
        <p>Some stuff in a paragraph</p> // Hi, it's me, the sibling. Oh, but wait, I also match B, so let's figure out if my sibling is a &lt;p&gt; symbol
        <p>Some stuff in a paragraph</p> // Hi, I'm that sibling
        <h3>Another heading</h3>    // Boo, I'm not a &lt;p&gt; sibling
        <p>Some stuff in a paragraph</p>    // Element that matches B, so go to next sibling
        <p>Some stuff in a paragraph</p>    // Hi, it's me, the sibling. Oh, but wait, I also match B, so let's figure out if my sibling is a &lt;p&gt; symbol
        <p>Some stuff in a paragraph</p>


## Colors
* RGBA and HSLA use opacity
    - Opacity of 0 is completely transparent, whereas an opacity of 1 is completely opaque
* Notice the different
    ```css
        /* Red with RGBA */
    p:nth-child(1) {
    background-color: rgba(255,0,0,0.5);
    }

    /* Red with opacity */
    p:nth-child(2) {
    background-color: rgb(255,0,0);
    opacity: 0.5;
    }
    ```

    - The first &lt;p&gt; will have *just* the background be transparent, whereas the second &lt;p&gt; will have *everything* be transparent, since you are explicitly stating that element's opacity
    - Good rule of thumb: RGBA for setting the background of something transparent (like a caption over an image), but still need readable text -- opacity for animations


## Cascade and Inheritance
* CONFLICTING ORDER: I call this the "order of operations of CSS", such that the first bullet here gets applied, then the second, then the third
    1. The user agent's (browser) default styling
    2. The declarations in a user's stylesheet (the person visiting the website)
    3. Author's stylesheet declarations (the web developer's .css files)
    4. The `!important ` declaration in a an author's (web developer's) .css files
    5. A user (website visitor's) `!important` stylesheet declarations
        - this would be for people who are visually impaired and need things like larger text to always appear
### Specificity
* The order
    1. `!important`
        - USE CASE: You assign an element an ID of #spcial that looks like this:
            ```css
            #special {
                background-color: green;
                border: 2px solid red;
            }
            ```
        - But, it's also part of a box class that looks like this:
        ```css
        .box {
            background-color: none !important;
        }
        ```
        - Even though the class is a *lower specificty* than the id, it will **still override** because it is an `!important` declaration
        - You also as
    2. ids (#idName)
    3. classes (.className)
    4. element tags (<p>)
* "Specificty" is just a calculation to determine how specific something is





