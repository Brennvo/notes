# **THESE HAVE NO STRUCTURE**

## These are just snibbets of things I find important to look back on/reference in the future.

* Changing an `<img>` to `display: block;` removes it from its default inline property
* Width
    - `max-width: 100%` on something like an `<img>` will scale the image to fit the width of its container, **but the image won't stretch wider than its original width**
    - `width: 100%` will stretch the image to the full 100% of its parent
    - Example] We have an image that is 1200px in a `<div>`
        * If image > container, then it exceeds the parent `div`
        * If image > broswer window, then browser adds a horizontal scroller
        * If you set the width as such:

            > img {
            >    width: 600px;
            > }

            , then it will stay *fixed* at 600px, regardless of its container
            - **this is a probelm if our browser size is only 320px for ex**
            

