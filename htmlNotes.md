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
    - Use the `<sup>` and `<sub>` keywords
    
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
    - [Fantastic article that talks about `srcset` and `picture`](https://www.sitepoint.com/how-to-build-responsive-images-with-srcset/)
    - `sizes: 50vw` tells the DOM how large the image will be relative to the user's viewport width
* Give your tables `<caption>` tag to explain what the table is to screen readers
    - It goes directly beneath the `<table>` tag
* Use `scope` attribute on `<th>` to specify that something is a header for either a column or row
    - this means the screenreader would know if you had the row acting as a column and vice-versa

### Forms

* `action` is where the form data will be sent
* the `for` attribute in the `<label>` element references the ***ID*** of the `<input>` element it is a label *for* (if somebody is actually reading this besides myself, I hope you like that pun)
* `<fieldset>` is how you create a group of widgets that share a similar purpose
    - adding a `<legend>` elmeents below the `<fieldset>` tag explains its purpose

    ```html
        <form>
            <fieldset>
                <legend>Fruit juice size</legend>
                <p>
                <input type="radio" name="size" id="size_1" value="small">
                <label for="size_1">Small</label>
                </p>
                <p>
                <input type="radio" name="size" id="size_2" value="medium">
                <label for="size_2">Medium</label>
                </p>
                <p>
                <input type="radio" name="size" id="size_3" value="large">
                <label for="size_3">Large</label>
                </p>
            </fieldset>
        </form>
    ```

    <blockquote cite="developer.mozilla.org">When reading the above form, a screen reader will speak "Fruit juice size small" for the first widget, "Fruit juice size medium" for the second, and "Fruit juice size large" for the third.</blockquote>

    * If you give a browser an input that it doesn't know, it will default to `type="text"`
    * To allow users to select multiple options in a `<select>` tag, use the `multiple` attribute

        ````html
        <select multiple id="multiple">
            <option>Banana</option>
            <option>Carrot</option>
            <option>Coffee</option>
        </select> 
         ```
    
    * for `<input type="number">` you can specify how much you want the button incrementer to increment by providing a `step` attribute

        ```html
        <input type="number" step="4">`
        ```
    * [Good article on CORS](https://www.codecademy.com/articles/what-is-cors)
    * HTTP Flow
        1. Open TCP Connection in one of the following manners:
            - new connection
            - resuse existing connection
            - open serveral connections
        2. Send an HTTP message
        3. Read the response from the server