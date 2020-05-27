## Basics

*It's advised to read up first on the Display property, which you can do right [here](/fundamentals.md)*.

### What's a box?
 
> Everything has a box around it in CSS. [MDN doc](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model)

That's quite easily seen by highlighting an element in your inspector and seeing it light up on your page. No matter how you look at it, it's gonna be a box.

Well this box is comprised of a few boxes of its own, although they are mostly at first hidden from view: 

- <span style="color: rgb(136, 197, 218);">Content box</span>: The area where your content is displayed. By default, this is what the `width` and `height` you are setting impact.
- <span style="color: rgb(120, 211, 120);">Padding box</span>: The padding sits around the content as white space; its size can be controlled using padding and related properties.
- <span style="color: rgb(255, 191, 16);">Border box</span>: The border box wraps the content and any padding. Its size and style can be controlled using border and related properties.


Lastly there is the Margin box. The margin is the outermost layer, wrapping the content, padding and border as whitespace between this box and other elements. No matter which `box-sizing` you might choose, a `margin` is always on the exterior of the element and never gets impacted (or impacts) its `width` or `height`.

Here's a typical representation of a CSS box: 

<div style="display: flex; justify-content: space-around;">
    <div style="width: min-content;" class="codeExampleContainer">
        <div class="box-model__example__color-boxes box-model__example__color-boxes--one">Content</div>
    </div>
</div>

### Changing the `box-sizing`

Now, it's not very convenient for the `width` and the `height` property that we set to an element not to take into account the <span style="color: rgb(120, 211, 120);">Paddings</span> and <span style="color: rgb(255, 191, 16);">Borders</span> of the element.

To remedy to that, CSS has a property: `box-sizing` which can be set to either `content-box` or `border-box`.

Its default value is, as said previously, `content-box` but setting it to `border-box` allows us to have the sizes of the paddings and borders to be substracted from the desired width first, before calculating the remaining width of the `content` box. 

**Good to note**: Margins are not taken into account in `border-box`, as the name implies (it stop at the `border` box).

*Trivia*: You might ask yourself why we would ever work with `content-box`. The [MDN doc](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing) gives a possible answer:
> When using `position: relative` or `position: absolute`, use of `box-sizing: content-box` allows the positioning values to be relative to the content, and independent of changes to `border` and `padding` sizes, which is sometimes desirable.



### Margin-collapsing

Margin-collapsing is a phenomenom you might encounter when dealing with *adjacent* elements. When that occurs, the adjacent margins of those elements get merged in a single one which takes the value of the bigger of the two margins.

Here, we declare on the top box a `margin-bottom: 30px;`, and on the bottom one a `margin-top: 50px;` and the result is a single 50px margin between those two boxes. 

<div style="display: flex; justify-content: space-around; align-items: center;">
    <div style="width: min-content;" class="codeExampleContainer">
        <div class="box-model__example__color-boxes box-model__example__color-boxes__margin-collapsing--one">Content</div>
        <div class="box-model__example__color-boxes box-model__example__color-boxes__margin-collapsing--two">Content</div>
    </div>
</div>

Now it is good to note that although the specs mention that this occurs for ["adjacent elements"](), this does **not** apply to `inline` elements, as you can see in action here, with a respective `margin-right: 80px` and `margin-left: 90px;`. The result is clearly not a 90px margin between the two boxes: 
<div style="display: flex; justify-content: space-around; align-items: center;">
    <div style="width: fit-content;" class="codeExampleContainer">
        <div style="display: inline-block;" class="box-model__example__color-boxes box-model__example__color-boxes__margin-not-collapsing--one">Content</div>
        <div style="display: inline-block;" class="box-model__example__color-boxes box-model__example__color-boxes__margin-not-collapsing--two">Content</div>
    </div>
</div>