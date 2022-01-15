# 02.Understanding CSS

## 0005. css-anatomy-terminology

- an example
  ```css
  p {
    color: #44444;
    font-size: 21px;
  }
  ```
- Here, `p` is a selector
- `color` and `font-size` are properties
- `#44444` and `21px` are value
- the line property and value is called `declaration`
- the whole example is called rule

## 0006. why-is-css-so-weird-an-introduction

- css is not broken
- css works the way it suppose to work
- learn Why Is CSS So Weird? by Miriam Suzanne https://www.youtube.com/watch?v=aHUtMbJw8iA
  - CSS is designed not to loose content and not cause harm
  - there are lots of devices which means the canvas is exactly known
  - css is there just to suggest how the content should visible
  - the default behavior is not to loose any content, thats why we see overflow content

## 0007. why-is-css-so-weird-a-follow-up

- website and web apps needs to device agnostic, means needs to work regardless of any device
- in early period of css there was pixel perfect design
- then we needed to maintain two css, one for main site and the other is mobile version
- then the responsive design came
- then the web needs to work everywhere
- it not the publisher who control how to display content, Its the audience
  - phone
  - tv
  - screen reader
- browser, device and the user can affect the output
- we have lots of variable- screen size, browsers and type of input
- We're designing for changing and adaptability
- css is written for a world where the creator doesn't have all the information
- we need to describe the intent of the outcome
- we need to make pages that can work without css
- ### css isn't broken when things don't act like you expect them to
- It usually means we simply need to try a different approach, because it has a very good reason for doing what it does(at least most of the time)

## 0008.css-is-all-about-relationships

- every component is connected and have effect in view
- The relationships between:
  - an element and the view port
  - an element and its parent
  - Sibling elements
- We need to take into consideration its relationship
  - Maybe its parent is defining a width instead?
    - If the parent has a width and we declare a width to the child, it might overflow out the side, or it might be a percentage of the parents's width
  - these relationships are controlled by a given elements formatting context
- css is all about relationship between elements we cannot think a component as isolated

# 03.Overlooked Fundamental 1- The box model

## 0009. introduction-to-the-overlooked-fundamentals

- css has global scope
- if components need to isolated then it is not reusable in the sense of css
- css has relationship with html, we can change style just adding class to html
- global scope of css is not a bug its feature so that we can reuse code
- we need to stop worried about global scope, if we understand it we can use it as our advancement

## 0010. the-box-model-and-box-sizing

- an example

  ```css
  .element {
    width: 200px;
    padding: 20px;
    border: 5px solid #820b35;
    margin: 20px;
  }
  ```

  - here the actual width is (20+5+20)\*2+200=290px
  - because the width is for content, so padding order and margin is adding up

- to solve this problem we can use `box-sizing:border-box`
  ```css
  .element {
    box-sizing: border-box;
    width: 200px;
    padding: 20px;
    border: 5px solid #820b35;
    margin: 20px;
  }
  ```
  - using this code the width will be content+padding+border, it will not include margin
  - ### with border-box, margin is not included, because the margin is between two element, if two element has 10px margin than there will be 10px gap not 10+10 = 20 px
- so we can use this css rule to be safe in our design

  ```css
  *,
  *::before,
  *::after {
    box-sizing: border-box;
  }
  ```

  - ### margin can impact another element is a big deal.
  - Intrinsic and extrinsic sizing (learn more in "bonus materials" section)

## 0011. what-happens-when-we-don't-set-a-width

- when we don't set a width to block element then the element take whole width of view or the container, even after adding padding and border it does not overflow but take space from the content
- this is without `box-sizing:border-box`

## 0012. what-happens-when-we-set-a-width

- ```css
  .content {
    border: 50px solid red;
    padding: 50px;
    margin-top: 10em;
    background: white;
    box-shadow: 0 0 3em rgba(0, 0, 0, 0.15);
  }
  ```

- without width default is `width:auto`
- when width is set to `100%` then the content width will be 100% of parent element, that case whole element will be more then 100% so that element will overflow

## 0013. adding-box-sizing

```css
 .content {
   box-sizing:border-box;
   width:100%
   border: 50px solid red;
   padding: 50px;
   margin-top: 10em;
   background: white;
   box-shadow: 0 0 3em rgba(0, 0, 0, 0.15);
 }
```

- here with border box the 100% width will be including padding and border, so there will be no overflow unless there is any word that is with long character
- with border-box if there is no margin then the element will not overflow

## 0014. fixing-a-layout

- when we use main content with a side bar, and we give 70% to main and 30% to side bar, with added padding the whole body can overflow
- we can solve this problem by adding `box-sizing:border-box`

## 0016.Inheritance

- not everything is inherited, but there is a general rule of thumb
- Anything related to typography is inherited

  ```txt
    font-size
    font-family
    text-decoration
    color

  ```

- using this inheritance feature we set the common style for html, so that all child have same property

  ```css
  html {
    font-family: "really-nice-font";
    font-size: 1.125rem;
    font-weight: 400;
    line-height: 1.7;
  }
  ```

- nothing related to layout is inherited

  ```txt
    margin
    padding
    height
    width
    position

  ```

- The following do not inherit things like you’d expect them to

  -

  ```html
  <button>
  <input>
  <optgroup>
  <select>
  <textarea>


  ```

- We can make them inherit those properties if we'd like

  ```css
  button,
  input,
  optgroup,
  select,
  textarea {
    font-family: inherit;
  }
  ```

- Use this to your advantage(depending on the design of course)

  ```css
  a {
    color: inherit;
  }
  h2,
  h3,
  h4 {
    font-weight: inherit;
  }
  ```
