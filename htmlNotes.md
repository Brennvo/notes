# HTML Notes

* HTML special characters

    ![special chars](https://i.imgur.com/L41mXFt.png)

* It is a good idea to set the language of your webpage
    - ```html
        <html lang="en-US">
            ```
* Absolute URLs always point to the same location
    - http://wwww.example.com
* Relative URLs point to a location *relative* to the file you are linking *from*
    - Use when you can because absolute URLs require the browser to look up the real location on the server using the DNS
* When you want to "share" something on your webpage via. email, leave the `mailto:` blank

    ```html
    <a href="mailto:">Share with friends</a>
    ```
* Superscript and subscript is good for dates, math, and elements
    * Use the `<sup>` and `<sub>` keywords
    
    ```html
    <p>My birthday is on the 17<sup>th</sup> of August</p>
    <p>x<sup>2</sup>
    ```

* Can add titles to `<img>` tags for a hover description

    ```html
    <img src="somepath" title="description for hover">
    ```

* For images and captions, use `<figcaption>` inside of a `<figure>` element
* If you want to reference an SVG, but also a PNG in case a broswer doesn't support it, use the `srcset="image.svg"` to reference the SVG version, and then use the regular `src="image.png"` to rference the other type of image file you want to include
* srcset and how it works
    - [Article one that describes using `sizes`](https://www.sitepoint.com/how-to-build-responsive-images-with-srcset/)
    - `sizes: 50vw` tells the DOM how large the image will be relative to the user's viewport width