## Animations

We'll talk here about two types of possibilities to animate your website (shiny! moving!): `transitions` and `keyframes`.

In both cases, the way to think about animations is to think about a starting point that you are currently at, and the end point that you want to reach. You will describe those two states and as you may guess the animation will be about *how* you get from point A to point B, which will give the illusion of movement and thereby of *transitioning* from point A to point B.

### Animations through transitions

Transitions are an easy way to incorporate quasi animations in your style. They are quite easy to apply, but their main feature is that they require some kind of a trigger to apply. Think `:hover`, `:focus`,...

As stated before, we want to describe a starting point (let's call it A) and an end point (let's then go with B).

For example, this is my point A:
```css
.myDiv {
    width: 50px;
    height: 50px;
    background: red;
}
```
and this is my point B (my point A in a `:hover` state, if you will):
```css
.myDiv:hover {
    width: 1000px;
    background: green;
}
```
As you can guess, as is, this will make the div bigger and green on `hover` *but* this will be instantaneous, and can hardly be called a transition.

#### `transition-duration`

To introduce actual transitions, we'll use the `transition-duration` property. It allows you to set (in milli-seconds, please, although seconds are also a possibility) the length the transition is supposed to span.

So if you want your transition to take a whole second, the code from above becomes:

```css
.myDiv {
    width: 50px;
    height: 50px;
    background: red;
    transition-duration: 2000ms;
}
.myDiv:hover {
    width: 1000px;
    background: green;
}
```

You'll notice that we attach the transition to the *starting point* and this is in most case what you will want to do. But why?

This example showcases why that is, since given this code:

```css
.myDiv {
    width: 50px;
    height: 50px;
    background: red;
}
.myDiv:hover {
    width: 1000px;
    background: green;
    transition-duration: 2000ms; /*Transition on end point*/
}
```

You would get the following animation:

<div class="codeExampleContainer">
    <div class="transitions__endpoint-example__toAnimate">Animation on hover</div>
</div>

You can see here that triggering the animation works well one way but the return trip is not quite as smooth. 

Indeed, as soon as the `:hover` state is no longer applied (our condition to return back to our point A), the `transition-duration` property is no longer applied either.

The same example, but with this time the `transition-duration` correctly applied to the starting point gives us this much smoother return animation:


<div class="codeExampleContainer">
    <div class="transitions__startpoint-example__toAnimate">Animation on hover</div>
</div>

#### The other `transition-x` properties

But what if you only want some specific property(ies) to change throughout the transition and not all of them?

`transition-property` allows you to do just that and to specificy which property(ies) you want to target. It is used as such:

```css
.myDiv {
    width: 50px;
    height: 50px;
    background: red;
    transition-property: background, width;
}
.myDiv:hover {
    width: 1000px;
    background: green;
}
```

There are options given to you to parametrize your transition speed via the `transition-timing-function` property, and the most common are:

- `linear`: That's pretty explicit, the speed will stay constant.
- `ease-in`: This means that you start slow and finish fast. It's the **default** value.
- `ease-out`: Meaning you start fast, and finish slow, obviously.
- `ease-in-out`: A bit of both, you start and end slow, but the middle of your animation happens to be fast. You might have guessed that your speed function in that case is a Gaussian.

This provides an example of those properties in action when you hover over those boxes:

<div class="codeExampleContainer">
    <div class="transitions__container">
        <div style="width: 50%;"><div class="toAnimate linear">Linear</div></div>
        <div style="width: 50%;"><div class="toAnimate ease-in">Ease-in</div></div>
        <div style="width: 50%;"><div class="toAnimate ease-out">Ease-out</div></div>
        <div style="width: 50%;"><div class="toAnimate ease-in-out">Ease-in-out</div></div>
    </div>
</div>

*Trivia fact*: CSS also allows you to declare your own Bezier curve, though the `cubic-bezier(p1, p2, p3, p4)` function.

**Good to note**: there is a shorthand for the `transition-property`, `transition-duration` and `transition-timing-function`, and you can chain the transitions in it. It workd like this:

```css
.startingPoint {
    /* property duration timing-function delay */
    transition: width 1000ms ease-in 2s,
                opacity 500ms;
}
```

That last bit of the `transition` property is about the `transition-delay`. It acts as you would mostly expect and allows you to trigger the animation (and not only its visual rendering, which is the key distinction to take from this) X seconds later.


#### The follow up of this Animation section is about `keyframes` and can be found [here](/animations-keyframes.md) 