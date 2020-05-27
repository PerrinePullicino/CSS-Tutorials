## Before we begin

### Preface

This is intended as a guide through the basis of Cascading Style Sheet (CSS).
Throughout all of this cheat sheet, you can consider that the best resource available to go further on a topic is the [MDN doc](https://developer.mozilla.org/en-US/docs/Learn/CSS) about it. When that's not the case, I'll link to the one(s) I consider better or simply more in depth.


### Your new best friend: the inspector

Chrome and Firefox  both have excellent (albeit slightly different)  DOM and style inspectors.
Chrome is overall the default browsers for most people and it is in my opinion an excellent choice, but if you opt for Firefox, you might be interested to know that there is a [Dev Edition](https://www.mozilla.org/fr/firefox/developer/) of Firefox which gives you a *better version of their inspector* along with some cool stuff on the side.

Now let's go.


# Fundamentals

## Types, Classes, IDs

CSS allows you to target an element to style through 3 main types of selectors:

- The type of the element
- The class of the element
- The ID of the element

The **type** of the element corresponds to its `Html Tag`. Think `div`, `a`, `label` and so on. It looks like this:
```css
div {
    background-color: red;
}
```

The **class** of an element is a reserved HTML attribute you've added to it. It's meant to be reused throughout your code and it is advised to regroup functionalities in small CSS classes. Applying **multiple classes** to your components is a good practice and allows for more understandable CSS. Think about role separation.
Styling through a Class looks like this:

```html
<div class="redDiv">
    <label>A label</label>
</div>
```

```css
.redDiv {
    background-color: red;
}
```

The **ID** of an element is also a reserved HTML attribute you've added to it. But contrary to a class, its usage should be unique. IDs are a good way to single out a component that would otherwise only get its class' style applied to it.

```html
<div id="myDivToTheRight">
    <label>A label</label>
</div>
```

```css
#myDivToTheRight {
    position: absolute;
    right: 0;
}
```

### Other ways of accessing selectors

| Selector          | Meaning                                                            |
|-------------------|--------------------------------------------------------------------|
| element1,element2 | Selects all element1 and element2                                  |
| element1 element2 | Selects all element2 inside an element1                            |
| element1>element2 | Selects all element2 that are direct children of an element1       |
| element1+element2 | Selects all element2 that are placed immediately after an element1 |
| element1~element2 | Selects all element2 that are preceded by an element1              |

You'll often see `+` and `~` in particular at times where you want to target all elements from a list except (respectively) the first and the last one.

## Cascade, Specificity and Inheritance

### Specificity

If you're stumped on why a CSS rule is applied rather than the other shiny one you just created, chances are you've found yourself in front of a *specificity* problem.

#### What it is

When CSS has two rules that can be applied to an element, it's going to choose the one that has the most *specificity*. Basically that means the selector you described the most precisely wins. 
If two selectors have the same level of specificity, the last one you described will win, that's part of the cascade.

##### Order by default

For selectors of specificity level 0 (no nested selectors), the order goes:
```
Specificity(Type) < Specificity(Class) < Specificity(Id) < Specificity(Inline)
```
So having the following code:

```html
<div id="redDiv">
    <label>A label</label>
</div>
```

```css
#redDiv {
    background-color: red;
}

div {
    background-color: green;
}
```
will result in a red div.

Now when there actually is a specifity level greater than 0 (nested selectors), the one with the most steps will take over the others ones. Intuitively, it means that if you have the following code:

```html
<div id="myDiv">
    <label class="redLabel">A label</label>
</div>
```

```css
label.redLabel {
    background-color: green;
}

.redLabel {
    background-color: red;
}
```
the label will be green instead of red, because you have described it *more precisely* in the first instance than in the second one.

### Cascade and inheritance

It's called *Cascading* Style Sheet because some of the properties you apply to parent elements trickle down to their children. As you may guess, not all properties are by default inherited. That would be hell. Things like `color`, `background-color` and `font-*` usually are, but your `position`, `width/height` and overall relative (as in dependant on the flow) properties are not inherited.

A couple keywords (there are two more, go and have a look) you might want to know about this are:
- `inherit`: This allows you to inherit any kind of property, even those that are not by default thought of as inherited properties.
- `initial`: It applies the default style of the property to it, rather than compute the one coming from your stylesheet.

### The `!important` keyword

**Don't. Use. This.** Using the `!important` keyword to solve your specificity conflicts is an admission of weakness and should be cause for a rejection of any PR. It's usually a sure way of demonstrating that you do not understand how the CSS cascade actually works.

Legit reasons to use the `!important` keyword do arise however if you're dealing with external CSS code (from a React component, for example, or a Jekyll theme...), and where recreating the level of nesting needed for the style to apply would be a waste of time and could end up not being what you exactly need anyway.


## Position

The `position` property in a way helps you order your HTML elements. However, it is not and should not be a fix for poor HTML. If your HTML is poorly structured, you'll find yourself abusing the `position` and `float` properties, which is a sure sign that you should rethink everything.

That being said, this property is incredibly useful and more importantly it is with `display` at the core of how things are rendered in CSS. Here are its most common values:

- `static`: This is the CSS default layout, and it piles element one below the other, in the order they are described in your HTML.
- `relative`: It's actually not far from what `static` does, but it allows you to manipulate the `top`, `left`, `right` and `bottom` properties of the `relative` element... Crucially (and by opposition to `absolute`) the space for the element is still reserved and the `top`/`left`... coordinates start from that reserved space. In other words, you place the element statically, *then* you offset it. This is overall a useful property that is actually rather **bad to use on its own** as it becomes increasingly hard to position your elements without conflicts.
- `absolute`: This completely removes the element from the flow (! different from `relative`). You still manipulate `top`/`left` and so on BUT they now come from a different referential - a parent container that it references. That parent is the closest parent *that is not static* it can find. Do note that if you do not specify any `relative` or `sticky`,etc... parent, this will default to the `<body>`.


## Display

- `block`: A `<div>`'s default display. An element with `display: block;` will take the entire width given to it. (It essentially forces a new line above and below the element)
- `inline`: The default display of a `<span>`. It will take the minimum amount of space possible to be displayed, and to that effect, `inline` element share their space with others.
- `inline-Block`: An `<image>` default display. As an `inline` element, it will also try to take the least amount of space possible, but this time you can set the width and height of the element (inline elements can't have a width and height).
- `none`: Makes the content disappear (acts as if it doesn't exist - the space isn't reserved, it is not simply invisible)
- `flex` and `grid`: Special ones, with a bunch of characteristics, described later.

Code example to showcase the Display property:

<div class="codeExampleContainer">
    <div class="display__container">Block</div>
    <div class="display__container inlineElement">Inline</div>
    <div class="display__container inlineBlockElement">InlineBlock with specific width set</div>
    <div class="display__container inlineElement">Inline</div>
    <div class="display__container">Block</div>
</div>

## Pseudo-classes

Pseudo-classes tell you something about the state that your element is currently in. There are lists of pseudo-classes all over the internet, but mainly what you should remember is that they are shortcuts to what you could do with Javascript to target states like `:hover` and `:disabled`.

Pseudo-classes are used like this:

```css
.myClass {
    background-color: red;
    font-size: 20px;
}
.myClass:hover {
    background-color: green;
}
```

It's good to note that on `:hover` this will give you a green element, but the `font-size` would still be the one defined in the simple `.myClass` selector, in accordance with the cascade principle.


For debug purposes, please experiment with your inspector about pseudo-classes: they are fully able to emulate a lot of the important states without you actually acting on the element. In essence, that means they can apply pseudo-classes state to an element without you meeting the requirements to do so.

## Pseudo-elements

When we talk about pseudo-elements (p-e), we talk about the `::before` and `::after` elements. Do note the two colons before the element itself, to conform to the newer way of writing CSS, efficiently distinguishing between a pseudo-class and a pseudo-element.
When attached to an element, the `::before` p-e gets displayed before what is inside that element, and the `::after` gets displayed after the inside of the element. This is actually crucial and explains why you cannot have a p-e in an `<input />` for example. To be able to have a p-e, an element must be able to have something inside of it, ie to have a content.

To be displayed, pseudo-elements *requires* to be given a `content` property. That `content` can be meaningful (actually displaying something), or it can be the empty string to allow its simple rendering.

No matter how you use them, you can only have one p-e of each kind on each valid HTML element.

## Media queries

Media queries allow you to morph your code depending on some screen requirements. In essence, they allow you to change the way things are displayed depending on some external factors.

They apply to three types of *media*:

- screen
- print: When you try to print a webpage
- speech: Speech synthesizer

and/or any number of *features* such as `width`, `orientation` and so on.`

You can combine types and features this way:

```css
@media print and (max-width: 500px) {
    //
}
```

The important syntax points to note are that you can express an AND condition and an OR condition (respectively) via code such as:

```css
@media(max-width: 500px) and (min-width: 200px) {
    //
}
```
and
```css
@media(max-width: 500px), (min-width: 200px) {
    //
}
```

You can also for convenience purposes use a `not` keyword that allows you to invert the meaning of the *entire* query.


## CSS functions

### `calc()`

Because maths is too hard, and also because it's useful. In that order. The `calc()` function allows you to compute calculations. You'll often find it inline with your CSS properties, like so:
```css
.class {
    width: calc(100% - 30px);
}
```
but giving the calculation meaning through a named variable is absolutely possible.
As you can see in the example, the best use of `calc()` comes from the fact that you can mix and match units!

Useful resources about it include this [complete guide to `calc`](https://css-tricks.com/a-complete-guide-to-calc-in-css/).
