# **THESE HAVE NO STRUCTURE**

## These are just snibbets of things I find important to look back on/reference in the future.

* Changing an `<img>` to `display: block;` removes it from its default inline property setting
* `width` vs. `max-width`
    - `max-width: 100%` on something like an `<img>` will scale the image to fit the width of its container, **but the image won't stretch wider than its original width**
    - `width: 100%` will stretch the image to the full 100% of its parent
    - Example] We have an image that is 1200px in a `<div>`
        * If image > container, then it exceeds the parent `div`
        * If image > broswer window, then browser adds a horizontal scroller
        * If you set the width as such:

            ```css
            img {
                width: 600px;
            }
            ```

            , then it will stay *fixed* at 600px, regardless of its container
            - **this is a probelm if our browser size is only 320px for ex**

        * How we should implement:
            ```css
            img {
                width: 100%;
                max-width: 700px;
            }
            ```

            * says that the fixed width of the image should take up entire size of parent element, **unless** it is greater than 700px

            * [video example here](https://youtu.be/2dha0BosQ6E?t=341)

* Flexbox 101
    * The two pivotal axis to flexbox
        1) Main axixs: defind by `flex-direction' (either row or column)
            * Row main axis = horizontal
                
                ![row main axis](https://mdn.mozillademos.org/files/15614/Basics1.png)

            * Column main axis = vertical
                
                ![column main axis](https://mdn.mozillademos.org/files/15615/Basics2.png)

        2) Cross axis: whatever is perpendicular to the main axis
            * Row cross axis = vertical
            * Column cross axis = horizontal
    * `align-tems` aligns items on the **cross axis**
        * initial value is `stretch`, meaning with `row`, it will take up the entire height
    * `justify-content` aligns items on the **main axis**
    * Start and end lines
        * When `flex-direction: row`, then the start edge is on the left, and the end edge is on the right (this is due to the English language -- in Arabic, it is reversed, however)
        * If you do `flex-directoin: row-reverse`, the start and end lines are now on the opposite sides (start is on the right, and end is on the left)
    * The container
        * by making the container `display: flex`, all of the container's children become **flex items**
    * Flex wrap
        * **By default, all flex-items will fit in the same row due to the initial felxbox values that allows the items to shrink. If the items were NOT allowed to shrink, there would be an overflow**
    * `flex-flow` is `flex-direction` followed by `flex-wrap`
    * If an item doesn't have an explicit size, such as `height` or `width`, then the size of the content itself (such as text in a box) will determine the `flex-basis`, aka theh default size
    * Good [article](https://css-tricks.com/flex-grow-is-weird/) on `flex-grow`, and yet [another](https://medium.freecodecamp.org/even-more-about-how-flexbox-works-explained-in-big-colorful-animated-gifs-a5a74812b053) describing it even better (go to flex-grow section)
        * You divide up the available space based on how many `flex-grow`s you are doing
    * `align-content` vs `align-items` article [here](https://stackoverflow.com/questions/31250174/css-flexbox-difference-between-align-items-and-align-content)


    

* [Good example of `justify-content` in Flexbox](https://learn.freecodecamp.org/responsive-web-design/css-flexbox/align-elements-using-the-justify-content-property)

* [Flexbox playground cheat sheet](https://codepen.io/enxaneta/full/adLPwv/)

* [A codepen that I made in order to show how you can leverage both `align-items` and `justify-content`](https://codepen.io/Hankis/pen/QYvKbN?editors=1100#0)
    * For `flex-direction: row;`
        * `align-items` moves the boxes on the y-axis (up and down)
        * `justify-content` moves the boxes on the x-axis (left and right)
    * For `flex-direction: column;`
        * `align-items` moves the boxes on the x-acis (left and right)
        * `justify-content` moves the boxes on the y-axis (up and down)

* Flexbox: `align-items` vs. `align-content`
    * `align-items`: this is what aligns the items as a *whole* within the container
        * Think of it as aligning everything in a PowerPoint document relative to the background of that PPT slide (all the content shifts)
    * `align-content`: determins the spacing between lines