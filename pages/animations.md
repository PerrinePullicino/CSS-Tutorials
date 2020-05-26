## Animations

### Animations through transitions

Transition are an easy way to incorporate quasi animations in your style. They are quite easy to apply.

The way to think about transitions is to think about a starting point that you are currently point, and the end point that you want to reach. You will describe those two states and as you may guess the *transition* will be about *how* you get from point A to point B, which will give the illusion of movement (*aka* animation) and thereby of *transitioning* from point A to point B.

For example, this is my point A:
```
.myDiv {
    width: 50px;
    height: 50px;
    background: red;
}
```
and this is my point B (my `pointA:hover`, if you will):
```
.myDiv:hover {
    width: 1000px;
    background: green;
}
```
As you can see, this will make the div bigger and green on `hover`.

Now this will be instantaneous, and can barely be called a transition. This is why you'll get to use the `transition-duration` property! It allows you to set (in milli-seconds, please, although seconds are also possible) the length the transition is supposed to span.

So if you want your transition to take a whole second, the code from above becomes:

```
.myDiv {
    width: 50px;
    height: 50px;
    background: red;
    transition-duration: 1000ms;
}
.myDiv:hover {
    width: 1000px;
    background: green;
}
```

But what if you only want some specific property(ies) to change throughout the transition and not all of them?

`transition-property` allows you to do just that and to specificy which property(ies) you want to target. It is used as such:

```
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

There are four cut options given to you to parametrize your transition speed via the `transition-timing-function` property:

- `linear`: Pretty explicit, the speed will stay constant.
- `ease-in`: This means that you start slow and finish fast.
- `ease-out`: Meaning you start fast, and finish slow, obviously.
- `ease-in-out`: A bit of both, you start and end slow, but the middle of your animation happens to be fast. You might have guessed that your speed function in that case is a Gaussian.

This provides an example of those properties in action when you hover over those boxes:


<iframe id="transitionStyleExamplesFrame"
    title="Transition Examples"
    scrolling="no"
    src="https://perrinepullicino.github.io/CSS-Tutorials/code-examples/transitions.html">
</iframe>