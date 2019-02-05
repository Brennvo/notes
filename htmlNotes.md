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

    ````html
    <a href="mailto:">Share with friends</a>
    ````