## Flexbox

*The very best documentation I've read on `flexbox` is still the one from [CSS-Tricks](https://css-tricks.com/snippets/css/a-guide-to-flexbox/). I do recommend having a go at the [CSS specifications](https://www.w3.org/TR/css-flexbox-1/) about them, too. It is excellent, but a much bigger read.*

*Please note that the [box-model](../basics/box-model.md) discussion is advised before reading this.*

### What's a `flexbox`? 

In its most reductive definition, `flexbox` is an answer from CSS as to how to properly organize one dimensional layouts. In other words, whenever you deal with a row or a column, chances are that you might want to consider using a `flex` display. By contrast, `grid` is a two dimensional tool.

**A word of caution before we begin**: `flex` is very useful, and as a result it tends to be overused and can introduce undesired side effects. Although it is the better option when trying to emulate a row behavior, it is often advised to consider other options when trying to play with columns, as elements tend to have a `block` display (and therefore go directly below one another, as a column does).
 
We mentioned in the box-model discussion that a container has essentially two different kind of `display`, an outer one and an inner one. The outer one decides how the container itself behaves in relation to other elements of the flow, whereas the inner display mode tells you about how the elements inside the container behave. Pretty intuitive.

So talking about a `flexbox` as en element (like we do about "a `div`" for example) is misleading. We are actually talking about an element which outer display type can be set to `block` (**its default value**) or `inline`, but which inner display type is set to `flex`. By extension, the `inline-flex` value for your `display` property is actually a way for you to specify that you want your outer `display` type to be `inline` instead of block, whereas your inner `display` should be kept to `flex`.

```css
.myFlexboxDiv {
    display: inline-flex;
}
```

Which makes the overall container behave like an `inline` element.

<div class="codeExampleContainer">
    <span style="background-color: orange">Text outside a flexbox</span>
    <div style="background-color: lightyellow;"  class="flexbox-basics__inline-outer__container">
        <span>Text inside an inline flexbox</span>
    </div>
    <span style="background-color: orange;">Text outside a flexbox</span>
</div>

### Flex-direction

<div class="codeExampleContainer">
    <div class="flexbox-basics__all-types__container">
        <div>
            <div style="color: white; text-align: center;"> row </div>
            <div class="flexbox-basics__all-types__box  flexbox-basics__all-types__row">
                <div class="flexbox-basics__all-types__element">1</div>
                <div class="flexbox-basics__all-types__element">2</div>
                <div class="flexbox-basics__all-types__element">3</div>
            </div>
        </div>
        <div>
            <div style="color: white; text-align: center;"> column </div>
            <div class="flexbox-basics__all-types__box flexbox-basics__all-types__column">
                <div class="flexbox-basics__all-types__element">1</div>
                <div class="flexbox-basics__all-types__element">2</div>
                <div class="flexbox-basics__all-types__element">3</div>
            </div>
        </div>
        <div>
            <div style="color: white; text-align: center;"> row-reverse </div>
            <div class="flexbox-basics__all-types__box flexbox-basics__all-types__row-reverse">
                <div class="flexbox-basics__all-types__element">1</div>
                <div class="flexbox-basics__all-types__element">2</div>
                <div class="flexbox-basics__all-types__element">3</div>
            </div>
        </div>
        <div>
            <div style="color: white; text-align: center;"> column-reverse </div>
            <div class="flexbox-basics__all-types__box flexbox-basics__all-types__column-reverse">
                <div class="flexbox-basics__all-types__element">1</div>
                <div class="flexbox-basics__all-types__element">2</div>
                <div class="flexbox-basics__all-types__element">3</div>
            </div>
        </div>
    </div>
</div>

### Main-axis, cross-axis/justify-content, align-items

A `flex` container has a main and a cross axis. The main axis goes along the `flex-direction` and the cross axis is perpendicular to the main axis. 

So a `flex-direction: row` container will have an horizontal main axis and a vertical cross axis.

There are two CSS properties meant to align things on the main and cross axis. Respectively, they are `justify-content` and `align-items`. [Here](https://jsfiddle.net/nhc50Lba/38/)'s a playground to help with the visualization of the values those properties can take.


### `flex-wrap`

By default, you won't have any wrapping ability attached to your `flex` container, and it will try as much as possible to fit all your components on a single line/column by squashing them. If you however want things to collapse, a `flex-wrap` property is available. Here's what it looks like in action:

<div class="codeExampleContainer">
    <div class="flexbox-basics__flex-wrap__container">
        <div>
            <div style="text-align: center; color: white;">No Wrap, 290px flex container</div>
            <div class="flexbox-basics__flex-wrap__no-wrap">
                <div class="flexbox-basics__flex-wrap__element">100px wide element</div>
                <div class="flexbox-basics__flex-wrap__element">100px wide element</div>
                <div class="flexbox-basics__flex-wrap__element">100px wide element</div>
            </div>
        </div>
        <div>
            <div style="text-align: center; color: white;">With Wrap, 290px flex container</div>
            <div class="flexbox-basics__flex-wrap__with-wrap">
                <div class="flexbox-basics__flex-wrap__element">100px wide element</div>
                <div class="flexbox-basics__flex-wrap__element">100px wide element</div>
                <div class="flexbox-basics__flex-wrap__element">100px wide element</div>
            </div>    
        </div>
    </div>
</div>