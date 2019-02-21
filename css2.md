# CSS Notes

## Introduction to CSS
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

### Attribute Selectors
* Value attribute selectors
    - `[attr]`
    - `[attr=val]`: only if the attribute has a value of `val`
    - `[attr~=val]`: if the attribute's value contains `val` somewhere in it
* Substring value attribute selectors
    - substring in this context is this: "cat" is a substring to "caterpillar"
    - `[attr^=val]` *and* `[attr|=val]` attribute must **START** with `val`
    - `[attr$=val]` attribute must **END** with `val`
    - `[attr*=val]` attribute must **CONTAIN** `val` in it

### Pseudo-classes and pseudo-elements
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



#### `(an + b)` psuedo-class selector formula
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

### Combinators

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


### Colors
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


### Cascade and Inheritance
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


### Inheritance
* What IS inherited: font-family, color
* What IS NOT inherited: margin, padding, border, background-image

### Box Model
* [Margin collapse Stackoverflow explanation](https://stackoverflow.com/questions/7168993/how-do-nested-vertical-margin-collapses-work)
* When do elements *not* collapse?
    - Positioned elements
        - Absolute
        - Fixed
    - Floated and cleared elements
    - Inline-block elements
    - Overflow set to anything (**except** visible)
* [Great video on margin collapsing, which is what I reference below in my notes](https://www.youtube.com/watch?v=7D6RyTIBk08) 
* When **do** they collapse?
    - Vertical margins of two vertically adjacent elements
    - Vertical margins collapsign between the parent and child element
        - **only the first and last child**
        - The only time this won't collapse is when there is a padding, border, or content in the parent element
            - What **should** happen:
                ![This is what should happen](https://imgur.com/a/HttuFsz)
            - What **should not** happen:
                ![This is what should NOT happen](https://imgur.com/a/Oh4Izna)
* Content's width is defaulted to be 100% of the avilable space (after the margin, border, and padding have taken their share)
* `background-clip` is how you determine how far an image extends out to the edge of the border
    - [MDN outlines this pretty well in their example](https://developer.mozilla.org/en-US/docs/Web/CSS/background-clip)


### Types of boxes
* `block`
* `inline`
    - Width and height settings have no effect on the `inline` boxes
* `inline-block`
    - flows like `inline`, but **can** be sized using width and height

![example](https://i.imgur.com/oTTcsdo.png)

* The first line: `inline`
* The second line: `block`
* The third line: `inline-block`
    - this is important: it started on a new line no because it has `block` in its name, but rather, due to it being inline, it was originally trying to fit on that first line of text after the first sentence. However, since is *is* a box, it's keeping that integiry, so it started it on a new line in order for the box to fit. As we see, it does still act as an `inline`, because there is still text coming right after the box
        - GREAT example by MDN! Kudos

----

## Styling Text

### Font styling
* [link to web safe fonts](https://www.cssfontstack.com/)
* The five generic web fonts and what they mean
    ![term, definition, and example](https://i.imgur.com/4hoFOjt.png)
* `font-size`
    - `em`s: 1em = font size of parent element of the current element
* Important note on `em`
    - Since the default value of HTML `font-size` is 16px, if you use `2em` it would compute to 32px
        - However, let's say we declare the `font-size` of a child element, such as `article`, to `font-size: 1.5em;`, which now computes to 24px
            - If we are to know specify the `font-size` of a `<p>` element nested inside of the `<article>` element, it would be **based off the `<article>` elements new `font-size` of 24.
                - Therefore, to get a computed font size of 20px, we need to use `0.83333333em`

* `text-decoration` is more interesting than you think
    - Values: `none`, `underline`, `overline`, `line-through`
        - *NOTE*: people generally prefer to use `border-bottom` for underlining for a couple of reasons
            - better styling
            - doesn't cut across the word is it "underlining", such as the tails on "g" and "y"
    - It accepts multiple values, and you can even style those values
        - `text-decoration-line`, `text-decoration-style`, `text-decoration-color`

### List styling
* Three important properties for styling lists
    1. `list-style-type`
        - square, circle, numbers, letters, roman numerals
    2. `list-style-position`
        - when the same bullet's text begins to run onto a new line, should that text be in line with the text above it, or the bullet it is underneath?
        - `list-style-position: outside`
        ![outside](https://i.imgur.com/KwdFPjI.png)
        - `list-style-position: inside`
        ![inside](https://i.imgur.com/B16DlaI.png)
    3. `list-style-image`

### Links styling
* Important to konw their psuedo-class states
    - Link (means it is univisited)
        - The default *state* that the link resides in (aka when it isn't in any other state)
    - Unvisited
        - Default color: blue
    - Visited
        - Default color: purple
    - Hover
        - Makes the mousepointer change to a hand icon
    - Focus
    - Active (when a link is being clicked on)
        - Default color: red
        - You can achieve this by holding down the mouse button, but not letting go
* The order you override the pseudo-classes matters
    - [Visit MDN to get the order](https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_text/Styling_links)

### Web Fonts
* Web fonts are a CSS feature that allows you to specify font files to be downloaded along with your websites as it is accessed -- this means any browswer that supports web fonts can have the exact font you want
* You specify a web font like this:
    ```css
    @font-face {
        font-family: "myFont",
        src: url("myFont.ttf");
    }

    html {
        font-family: "myFont";
    }
    ```
    - It's important to note that you can name the `font-family` anything you would like, just as long as you continue to refer to it that way throughout your CSS
* A good article on implementing `@font-face` and using the same `font-family` name for the same font style of text, but when you have downloaded different versions of it
    - Example] Say you download a font called 'DroidSerif' in its regular and bold version
        - Instead of naming each `font-family` to their respective names (DroidSerifRegular and DroidSerifBold), just name them both the same (DroidSerif), but then change the `font-weight` on each `@font-face` so that don't have to keep specifying `font-family` in your CSS when you want to use a specific version of DroidSerif

----

## Styling Boxes

### Box Model Recap
![box model](https://mdn.mozillademos.org/files/13647/box-model-standard-small.png)

* box heights adopt the height of the *content* inside the box, **unless** you give it an absolute height
* By default, `background-images` default to the outer edge of the box border
    - this means it overlays the padding **and** border
        - However, if you have an opaque border, the background-image will hide behind it
* To make a border without changing the size of the box, use `outline` -- it is drawn **on top** of the box
* **you CANNOT tamper with an `inline` box's width and height settings**
    - padding, margin, and border of these elements only affect the surrounding text, but **not** the surrounding block boxes
* To center a container inside of its parent: `margin: 0 auto;`
* Important and recursive example I always fall into
    * [Link for example](https://mdn.github.io/learning-area/css/styling-boxes/box-model-recap/min-max-container.html)
            - In this example, the image falls outside of its parent (the white box), and overflows onto the grey body
            - In order to make sure that the image stays within its parent, we need to do **three things**
                1. Set the image to `display: block;`
                2. Change the margins to center: `margin: 0 auto;`
                3. Set the max-width of the image so that it never falls out of its parent by doing `max-width: 100%` -- this makes sure it is only 100% of its parent and never gets larger (which it is doing in the link above)
                - [Here is the new example](https://mdn.github.io/learning-area/css/styling-boxes/box-model-recap/min-max-image-container.html)

#### Total width of box = `width` + `padding-right` + `padding-left` + `border-right` + `border-left`
* This formula can get annoying, so we can change it up using `box-sizing`
* **When we change the `box-sizing: border-box`, we make the box model's `height` and `width` now include the content, padding, and border (as opposed to just the content as we've been used to before)
    ![image to new box model](https://mdn.mozillademos.org/files/13649/box-model-alt-small.png)
    - [Codepen that explicitly shows this](https://codepen.io/pen/?&editable=true)
        - **NOTE**: the "width" being shown isn't a CSS value, it's a logical "width" that the box is taking up
            - This is important because in the top box, the actual `width` of the box is 300px since we aren't in `border-box` -- when we state `width: 300px` in the default `box-sizing` mode, we are explicitly stating the content's width, and **not** the entire box's width like we do in `border-box`

### Backgrounds
* A background of an element sits underneath the content, padding, and border
    - it doesn't sit underneath the margin, because the margin is technically the area *outside* the element
    - **unless** you specify the `background-clip` property as discussed before

* it is important to note that background images are for decorative purposes only
    - if your image in the background-image has meaning, make it an `<img>` so that assistive technologies actually understand there is a significant element on the page and provide a caption to it as well
* `background-position` takes different measurement units
    - percentage means how far along in the box it should be
        - Ex] `backgrounnd-position: 99% center` meanns 99% to the right of the box, then center it horizontally
* `background-attachment` is the behavior of the background image as the content scrolls (only when there is enough content to scroll)
    - `background-attachment: scroll` means the background scolls with the text
    - `background-attachment: fixed` means the background stays put as you scroll with the content

* [link to sports cards codepen](https://codepen.io/Hankis/pen/vbQQLB?editors=1100)

#### `background` properties for quick reference
![background properties for quick reference](https://i.imgur.com/gYnkn8S.png)

* **ALWAYS SET A BACKGROUND-COLORS AND FONT COLORS REGARDLESS OF WHETHER IT LOOKS GOOD WITHOUT ONE OR NOT**
    - [link explaining why due to new nightmode in browsers](https://www.luu.io/posts/web-devs-font-color)

### Borders
* `border-radius` can take different specificities

    ```css
        /* 1st value is top left and bottom right corners,
    2nd value is top right and bottom left  */
    border-radius: 20px 10px;
    /* 1st value is top left corner, 2nd value is top right
    and bottom left, 3rd value is bottom right  */
    border-radius: 20px 10px 50px;
    /* top left, top right, bottom right, bottom left */
    border-radius: 20px 10px 50px 0;
    ```

* `border-image` is a powerful way to get an image as the border, but the `border-image-slice` can be a bit confusing. [Here is an article that describes it best](http://thenewcode.com/438/CSS-Border-Image-Explained)

### Syling Tables
* `border-collapse: collapse;` is what brings borders from the default two lines to one, single line
* you can change where a caption is placed by using `caption-side`, which takes the following:
    - `bottom`
    - `top`


### Advanced box effects

#### Box shadows
* order
    1. horizontal offset (distance to right)
        - positive value => moves to right
        - negative value => moves to left
    2. vertical offset (distance downwards)
        - positive value => downwards
        - negative value => upwards
    3. blur radius
    4. base color
* when you stack box shadows, be sure that they are cascading such that you can actually see the next box
    - if you make one as such:
    ```css
    box-shadow: 1px 1px 1px black;
    ```
    your next shadow will need to be `2px` in order to see it

#### Filters
* Can be applied to any element (block or element) using the `filter` property
* `drop-shadow()` works on the actual *shapes* of the content inside the box, not just the box
    * NOT supported in IE

#### Blend modes
* Tell CSS what to do when two elements overlap
    - `background-blend-mode`: blends together multiple background iamges
    - `mix-blend-mode`: blends together the element it is set on with elements it is overlapping
        - **both** background AND content

## CSS Layout

### Introduction
* We use displays to manipulate the way something is displayed, while still keeping the semantic meaning of the element
    - For instance, having a `<li>` go from a block to an inline means we tell the markup it is still a list, however, we are manipulating its appearance

#### Flexbox briefing
* By default, the height of each item is streteched to the height of the tallest item, since the default value of `align-items` in `flex-direction: row` is `stretch`
* By doing `flex: 1` to our specific items in the flex, we tell it to:
    - grow and fill the container when there is enough space, but also shrink and become narrower if the space gets smaller
    - if you apply this to all the items, then they will adjust to take up the same amount of space evenly

### Normal Flow
* By default, a **block level** element's width and heigth are:
    - 100% the width of its parent element
    - as tall as their content
* By default, an **inlin element's** width and height are:
    - width is as wide as their content
    - height is as wide as their content
* CANNOT SET WIDTH AND HEIGHT ON AN INLINE ELEMENT
    - You have to forcibly change the behvaior by setting it to
        - `display: inline-block` or `display: block;`

### Flexbox
* shorthand for `flex-direction` and `flex-wrap` is `flex-flow`
    - `flex-flow`: flex-direction, flex-wrap
        - Ex] `flex-flow: row wrap;`
* `justify-content` is only when there is avialble space on the main axis
* Example]
    - parent width: 900px;
    - `<section>` width: 99px
    - `<aside>` width: 623px
    - total flex-grow values: 3
    - **Calculation**
        - Total elements take up: 99 + 623 = 722
        - Remaining space = 900 - 722 = 178
        - Divide how much **one** flex-grow is by dividing it by the total values of the `flex-grow` --> (`flex=grow: 2` + `flex-grow: 1`) = 3
            - 178 / 3 = 59.33
    - So, one `flex-grow` is 59.33
    - **Divy it up**
        - In our example, `<article>` has a flex-grow value of 2
            - `<article>` receives (59.33 * 2) = 118.66 space, **plus its additional width of 99**, which now evaulates to a total width of 217.66
        - `<section>` receives (59.33 * 1 ) = 59.33 + 623 = 682.33
* [Good article on flex-basis vs. width](https://gedd.ski/post/the-difference-between-width-and-flex-basis/)
* `flex-basis` on columns adjusts height, `flex-basis` on rows adjusts width
    - [link](https://technet.microsoft.com/en-us/windows/dn254946(v=vs.60))
    - [link](https://webplatform.github.io/docs/css/properties/flex-basis/)
    - [another link](https://stackoverflow.com/questions/34352140/what-are-the-differences-between-flex-basis-and-width)
    - [another link](https://stackoverflow.com/questions/46716277/flex-basis-not-expanding-width)

#### flex-grow explained
* when we normally do `display: flex;`, flex items are stacked horizontally and if there isn't enough space, they will shrink in size
* If there is more than enough space, however, we can have it distribute accordingly
1. Count how many `flex-grow`s there are
    - if you have a css selector such as `div { flex: 1; }`, then you need to include how many `<divs>` there are in your HTML so you can get the total amount


#### What does `flex: 1` mean??
* `flex: 1` is a unitless proportion that dictates how much of the available space along the main axis each flex item will take up
    - a value of 1 indicates that they will take up an equal amount of space along the main axis

#### Flexbox default values
* on the main axis, items **do not stretch**, but rather, take up the size of their content as the size in the main axis
* `align-items`, which aligns items on the *cross axis*, is automatically set to `stretch`
    - IF the flex-item has a parent, it will stretch to fill the parent's width
    - IF the flex-item *does not* have a parent, it will stretch to fill as long as the longest flex-item (basically, which ever flex item has the most text)
* All flex items have an `order` value of 0
    - So, that means, if you just give one of the flex items a positive value, it is viewed as the "end"
        - The same can be said about negative values as well
    - If some have the same values, then it is ordered based off of the source order
* When you have multiple items in a container that wrap around to multiple lines, you can define how that content is spread out line-per-line by specifying `align-content` in the container itself
* If items are too large to display on one line, they will shirnk to fit the container, or overflow if the items could not shrink small enough to fit


#### `justify-self` workaround
* Since Flexbox treats items along the main axis as a group, you cannot explicitly call out an item on there and have it justify itself alone
* the trick around this is to use margins
    1. Target the item you want to manipulate by giving it a class, id, etc.
    2. in your css, do the following
        ```css
        .targetItem {
            margin-left: auto;
        }
        ```
        This will effectively push the item to the right side of the screen since auto margins take up as much space as possible


#### `flex` shorthand = `flex-grow`, `flex-shrink`, `flex-basis`
* the default value is `flex: 0 1 auto`, which is also `flex: initial`
    - `flex-grow` of 0 means that it will *not* grow larger than their flex basis
    - `flex-shrink` of 1 means that items can shrink if they need to rather than overflowing
    - `flex-basis` of auto means that items will either use any size set on the item in the main dimension, or they will get their size from their content
* It is good to use `flex: auto`, which is equivalent to `flex: 1 1 auto`
    - This is the same as above, although now, the items are allowed to grow
* The shorthand you often see in tutorials is `flex: 1` or `flex: 2` and so on. This is as if you used `flex: 1 1 0`. The items can grow and shrink from a `flex-basis` of 0.
* **POSITIVE FREE SPACE** is when the flex containre has more space than is required to display the flex items inside the container
* **NEGATIVE FREE SPACE** is when the natrual size of the items add up to a total that is larger than the availabe space in the flex container
* When `flex-basis` is set to auto (which remember, is the initial value as per above), then it will take up the **max-content width**, so basically, it just gives it as much space as the content dictates
* When 'flex-basis` is 0, it uses the `min-width`, so it will take up the max length of the the text characters (or image, whatever have you)
* Example]
    - If you have items with a `flex: 1 1 auto`, you are saying that it can equally share growth space. However, it doesn't mean they will all end up being the same width, because since `flex-basis` in this shorthand is set to `auto`, it means that the width is equal to the `max-content` of the box
        - So, while they all get an equal share of the pie in regards to the available free space, the box with more content will still naturally appear larger due to having more content
    - ---> to avoid this, you set the `flex-basis` in the shorthand to 0 so that it starts out as min-width
* **what is important to remember on this is that this is all assuming we have free space. If I go into codepen in the link above and enter "sldjflkadsjflakdsjflaksdjfalksdflasdfjlsdkjfsljflsdjfakdsl" into the box, there won't be enough free space to see our examples since that box has so much content. It's better exemplified if you give a longer setence with spaces "content like this will work better in teh examples since min-content is much better than the min-content of the long string above"
* How `flex-shrink` works; broswer will see if the `flex-basis` can fit, and if not, it will shrink if you specify the `flex` to do so
* Go down to the [flex-shrink and flex-basis portion of MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Controlling_Ratios_of_Flex_Items_Along_the_Main_Ax) and toggle between these two `flex` values
    - `flex: 1 1 auto;`
    - `flex: 1 0 auto;`
** ITEMS ARE FLOORED IN FLEX-SHRINK TO THE SIZE OF THEIR MIN-CONTENT, SO THEY WON'T JUST START SHRINKING AUTOMATICALLY
    - [look at this codepen example](https://codepen.io/Hankis/pen/gqJjWj)
        - Notice how we have a red box that is centerd. We need all of the content inside of there.
        1. Set all `<divs>` to this:
            - `flex: 0 0 auto;`
        2. Change `.three` to `flex: 0 1 auto`;
            - Notice how it will now shrink the box so it fits within the red border.
        3. Change `.three` back to `flex: 0 0 auto` and instead change `.one` to `flex: 0 1 auto`
            - Notice how it won't do anything. It's not shrinking! This is because it **floors to the size of min-content** as we mentioend above. It can't do anything to reduce the box because it will not forgoe the integrity of its content for the sake of shrinking.

#### Important takeaways
* Flex basis rendering
    - If the flex-item has a `flex-basis` that is set to `auto` and the flex-item **does** have a defined width somehwere else in the code (such as 500px, 50%, etc.), `auto` refers to that size.
        - However, if there **is not defined width**, then `auto` is converts to the size of the content (and in the max-content fashion)
    - Giving a flex item a unit value, it will revert to that size
* Available space
    - The first thing to do is calculate how much space the flexed items are taking up so we can determine if `flex-grow` and `flex-shrink` will even come into play
        - If the added sum is > the container's width, then `flex-shrink` will come into play
        - If the added sum is < the container's width, then `flex-grow` will come into play
** **YOU DO NOT HAVE TO ADD EXTRA SPACE TO YOUR ITEMS IF YOU DON'T WANT, YOU CAN SIMPLY MOVE ITEMS AROUND INSIDE OF THE FREE SPACE ITSELF BY USING `justify-content` AS WE FIRST LEARNED**
    - all caps because this is importatnt. After learning a lot about `flex-grow` and `flex-shrink`, it makes it seem like you HAVE to distribute free space, but you **don't**. It's up to your requirements/vision
