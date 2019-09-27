# HTML CSS THREE

In this lecture we discuss media queries and animations.

## Responsive Design

Responsive design is the process of building an application's user interface (UI) to dynamically adjust based on the size of the device being used to access it.

Older websites were not designed with responsive design principles in mind, and this has lead to undesirable user experiences. Take a look at https://www.spacejam.com/archive/spacejam/movie/jam.htm for an example.

Nowadays, it is standard practice to ensure that websites are responsive. Some examples of responsive designs can be found here: https://www.awwwards.com/50-examples-of-responsive-web-design.html. 

The reason responsive design is important is because increasing numbers of users are consuming the internet via mobile devices or tablets. There are ~1.2 billion web users world wide, and ~48% of them primarily use the internet on their mobile device. Moreover, being capable of designing responsive sites is a requirement for any front-end developer position.

When building your application, there are three main devices to develop for. `mobile`, `tablet`, and `desktop`.

![resposive design](images/responsive.jpg)

### Extraction

The `extraction` design process of building an application is when developers start from `desktop` design, and then extract features until the design fits smaller devices.

The extraction design process often results in a desktop application that is rich with features, and a mobile application that feels like an ineffective afterthought. This is because it can be difficult to include all of the features from the desktop view when working with a mobile sized viewport. With extraction design, mobile views can be left feeling either cluttered and clunky, or less usable and effective than the desktop design.  

### Enhancement

The `enhancement` design process is when developers begin by deciding the core features and layout for the `mobile` view, and then "enhance" the application in order to fill out the  `desktop` design.

This will allow you to add features into your app as you scale up with the view port size. This is also known as `mobile first` development. This process more reliably results in a robust mobile view and an equally effective desktop design. 

In short, it's easier to scale up than it is to scale down.

## Media Queries

In CSS, we can use `media queries` to help create a `responsive design`.

A `media query` is a set of CSS rules that will apply to devices based on the viewport size of the device being used to access the page.

The syntax for writing a media query looks like the following:

```css
@media (max-width: 500px) {
    /* New Styles To Apply Based On Width */
    .navbar {
        background: tomato;
    }
}
```

Media queries are defined in CSS by using the `@media` statement. In the parentheses, we can specify the dimensions of the view port that our styles will apply to. The value passed into the parentheses can be referred to as a `break point`. Typically, break points are set with a `min-width` or `max-width` value. Inside the curly braces, we style normally. 


![break points](images/breakpoints.png)

### Min-Width

Min-width is the value used to declare the minimum width of screen size that the styling block will be applied to. This means that the styles will be applied when the view port width is higher than the `min-width` value.
 
```css
@media (min-width: 500px) {
    /* Styles will only be applied when view port width is 500px and above */
    .navbar {
        background: orange;
    }
}
```

### Max-Width

Max-width is the value used to declare the maximum point of screen width that the styling block would apply to. This means that the styles will be applied if the view port width is smaller than the `max-width` value.

```css
@media (max-width: 500px) {
    /* Styles will only be applied when view port width is 500px and lower */
    .navbar {
        background: orange;
    }
}
```

You can use `max-width` or `min-width` interchangeably, but it's best to stick with one or the other to make your code more clear.

## Animations

Animations are used to dynamically animate elements on our web page. When utilized well, animations enrich the user experience and keep users on a site. Check out https://www.theglyph.studio/#home for an example of a site that utilizes animations well. When utilized poorly, animations can be distracting and unpleasant, and can push users away. Take a look at https://www.lingscars.com/ for an example of what poorly utilized animations can look like.

There are a multitude of ways to achieve an animation effect on a webpage. One way animations can be created is by using `keyframes` in our CSS.

### Keyframes

To reiterate, keyframes are one method that can be used to create an animation via CSS. Keyframes are declared with `@keyframes`, followed by a name that can be used to reference the keyframe. The @keyframes CSS "at-rule" controls the intermediate steps in a CSS animation sequence by defining styles for keyframes (or waypoints) along the animation sequence. 

```css
@keyframes spin {
    
}
```

There are a couple ways that we can apply styles using a keyframe. One way is by using `from` and `to`. `from` and `to` can be used to define a set of style rules that specify the start and end state of an element in CSS.

```css
@keyframes spin {
    from {
        transform: rotate(0deg);
    }
    to {
        transform: rotate(180deg);
    }
}
```

Another way is by using percentages inside of the animation, which enables greater specificity and control over how the animation.

```css
@keyframes spin {
    0% {
        transform: rotate(0deg);
    }
    100% {
        transform: rotate(180deg);
    }
    0% {
        transform: rotate(0deg);
    }
}
```

Now that we have created the animation, we now need to tell an element to use it.

```css
.square {
    height: 75px;
    width: 75px;
    background: peachpuff;
    /* tells what animation to use */
    animation-name: spin;
    /* tell how long to run animation */
    animation-duration: 2s;
    /* specify how many times the animation should run */
    animation-iteration-count: infinite;
    /* we can change the animations direction */
    animation-direction: alternate-reverse;
    /* we can smooth our animations */
    animation-timing-function: linear;
}
```

Notice how these animations are always. We can set it up so that the animation will fire when a specific event like a click happens.

We can conditionally add CSS classes to add the animation. We need to add all of the animation properties into it's own class.

```css
.square-spin {
    animation-name: spin;
    animation-duration: 2s;
    animation-iteration-count: infinite;
    animation-direction: alternate-reverse;
    animation-timing-function: linear;
}
```

Then we will create state on our component and write a method that will change the value on state from true to false, or false to true. Then we will conditionally add the class to the element depending on what state is.

```js
export default class App extends Component {
  constructor(){
    super();

    this.state = {
      spinning: false
    };

  };

  animate = () => {
    this.setState({
      spinning: !this.state.spinning
    })
  };

  render() {
    return (
      <div>
        <div className={
          this.state.spinning ?
          'square square-spin'
          :
          'square'} 
          onClick={this.animate}></div>
      </div>
    )
  }
};
```

### Transitions

Transitions are another way we can animate our elements. This time, the animation will just be a simple transition that will allow us to create smooth transitions.

All we need to do is use the `transition` property on our css elements. We will just define how long we want to the transition to happen.

```css
/* Transition Circle */
.transition-circle {
    height: 50px;
    width: 50px;
    margin: 25px auto;
    background: salmon;
    /* transition property to change values */
    transition: .2s
}

.transition-circle:hover {
    transform: scale(1.1);
    border-radius: 50%;
}
```

This will allow us to create simple animations on events such as a hover.
