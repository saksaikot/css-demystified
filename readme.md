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
  - there are lots of devices which means the canvas is not exactly known
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

## 0017.A quick look at inheritance in action

- we should take advantage of inheritance, all typographical property which is related to font will inherit from parent, unless there is a browser default, for this a tag color is blue by browser thats why we need to explicitly write the color for a tag.
- if we put center on a tag it does nothing since it is a inline element and it takes the space of content

## 0018.A little project

- finished the project in 0018.A little project>01.1 answer
- there is also style guide which i did not follow

## 0019.A little project my solution

- line-height is unit less and related to font-size, so `line-height:1` is 1 em which is `1* font-size`
- for smaller font size line-height is bigger, and when the font-size bigger line-height is smaller

## 0020.A little project follow up

- 1 rem is 1 \* font-size of html root element or html tag,
- so if we set the font-size in html then all the rem value will increase
- ### so keep mind html font-size is important for rem unit

# 05.Overlooked Fundamentals 3. The Cascade

## 0021.Introduction to the cascade

- focus on cascade, how we should use it
- we should not separate or isolate of element style rather we should use the cascading feature in our advantage

## 0022.How well do you really know it

- example, what color will have in these 2 div

  ```css
  .red {
    background: red;
  }
  .blue {
    background: blue;
  }
  ```

  ```html
  <div class="red blue">
    <div class="blue red"></div>
  </div>
  ```

- it will be blue
- ### how it calculate which rule should be apply
  - 1. Origin and Importance
  - 2. Specificity
  - 3. Order of Appearance

## 0023.Importance and origin

- Origin and importance order

  - 1.user declarations with !important
  - 2. Author declaration with !important
  - 3. Author ( css in the page ) declaration
  - 4. User declaration
  - 5. User agent ( browser default) declaration

- so end of the day the user in control of how page should look
- never set font-size to html, then it can override user declaration

## 0024.Origin and font size implications

- just an example showing the bad effect setting font-size in html

## 0025.When animations and transitions get involved

- as css specification
  - 1. Transitions
  - 2. user declarations with !important
  - 3. Author declaration with !important
  - 4. Animation
  - 5. Author ( css in the page ) declaration
  - 6. User declaration
  - 7. User agent ( browser default) declaration
- in reality (chrome and later firefox)
  - 1. user declarations with !important
  - 2. Author declaration with !important
  - 3. Animation
  - 4. Transitions
  - 5. Author ( css in the page ) declaration
  - 6. User declaration
  - 7. User agent ( browser default) declaration

## 0026.Closing thoughts on importance

- there are few situation where we should use !important, like media query so that we can disable animation for small device
- in general we should avoid !important when it is not a specific case

## 0027.Specificity

- the rule is more specific ( h2 vs div.h2) wins
- in early learning steps, there is a suggestion that we should avoid specificity, which is called flat specificity
- to do that we use certain css naming convention
- so we don't need to think about specificity
- if no specificity issue then we can ignore Origin and Importance
- so there will be only `order of importance`
- but as teacher suggested that it is like keeping the learning wheel on as in learning riding cycle.
- if we learn correct then we can use this specificity in our advantages

## 0028.Fixing specificity issues

- example of how specificity make issue and how flat css solve the problem

- https://codepen.io/tkhuong/pen/jOMZwgp

## 0029.Calculating specificity

- https://specificity.keegan.st/ to calculate css specificity
- specificity calculation rules:
  - A. IDs `#container #main #sidebar`
  - B. Classes `.logo`, attributes `[type="text"]` and pseudo-classes `:visited :hover :active`
  - C. Elements `div` and pseudo-elements `::before ::after ::first-line`
  - `#container #main` will calculate 2A,
  - `navbar::before` will calculate 1B+1C
  - A>B>C, so 1A will win with 10B+10C
- ### Special Rules
  - When calculating CSS specificity values, ignore the universal (\*) selector.`* { color: black; }`
  - Only the selector inside the :not() pseudo-class (negation pseudo-class) is counted. The :not() pseudo-class itself does not get counted.`:not(#some-id) { color: purple; } ` Specificity 1A
  - In case of a tie, the selector that’s farthest down the stylesheet wins.

## 0030.Pricing cards introduction

- exercise is done in the folder

## 0031.A safe approach to css

- rewrite the css according to lesson
- BEM convention -`base element modifier`
  - example `plan__title--dark`
- keep the common property in base rule, then use the modifier class to update the changes
- also used a utility class text-accent which is a dry code and we can reuse the class

## 0032.Challenge pricing cards

- answer in the folder

## 0033.My solution pricing cards

- button rules have problem with a tag
- default a tag has default `display:inline`
- `display:inline` can not set height,margin, and padding can be set but does not change content height
- to solve this problem we can use `display:inline-block`

## 0034.Updated design

- tried to solve the design

## 0035.Updated design my solution

- used variable

  - variable are set in root element so that it cant be accessed globally `:root{}`
  - variable name start with `--` double dash `--my-variable`
  - to name the color added clr prefix `--clr-primary-100` here 100 is the color tone
    - 500 is base, 100 is lightest and 900 is darkest
  - to reuse the background color we takeout `--plan-light` to utilities ie- `--bg-light`
  - to use the variable `var(--variable-name)`
  - optionally we can add default value is variable is not defined `var(--variable-name,red)`
  - body,h1..h6,block elements have default margin, we need to reset or change the margin accordingly
  - we can use base with utility class to give separate style(ie separate bg,color)

    ```css
    button {
      margin: 0;
      padding: 2rem;
      border: 0;
      outline: 0;
      background: var(--bg-btn, black);
      color: var(--bg-clr, white);
    }
    dark-element {
      --bg-btn: white;
      --clr-btn: black;
    }
    ```

## 0036.Adding in custom properties

- already did in last commit

## 0037.Setting up the typography

-

## 0038.Mirroring the layout

- used modifier class to mirror the layout
- since the members is a flex layout we can change the order
- we changed the order to 2,
- we fixed the member padding and img left and right margin
- other fixed

  - the css is used two naming, one is bem and other is nesting
  - in bem

    ```html
    <div class="plan">
      <div class="plan__price plan--modifier"></div>
    </div>
    ```

  - without bem to use it as global component style
    ```html
    <div class="plan">
      <div class="price color-pop"></div>
    </div>
    ```

## 0039.Starting to think about class naming

- here talked about BEM naming convention and class separated by specificity
  - bem is for flat css that can be repetitive writing
  - we can use class separator
    - `<class="price"> <class="amount" /></>` we can style it by `.price .amount{}` using specificity along with strict the scope

## 0040.Overlooked fundamentals final project

- practice project
- ## border-radius with padding is evil, radius will overflowed by padding, so be careful when use it with padding
- selectors

  - descendant selector (space)
    - example `div p` select all p that is inside div including Descendant (or not direct child)
  - child selector (>)
    - example `div > p` select all p that direct child of div not Descendant (or not direct child)
  - adjacent sibling selector (+)

    - example `div+p` select immediate sibling that is only p
    - example

      ```html
      <div>
        <p>Paragraph 1 in the div.</p>
        <p>Paragraph 2 in the div.</p>
      </div>

      <p>Paragraph 3. will be selected here</p>
      <p>Paragraph 4. After a div.</p>
      ```

  - general sibling selector (~)

    - example `div~p` select all siblings those are p and after div, this is only direct sibling
    - example

      ```html
      <div>
        <p>Paragraph 2.</p>
      </div>

      <p>Paragraph 3 will select</p>
      <section><p>Some code is not select by the selector</p></section>
      <p>Paragraph 4 will select</p>
      ```

## 0041.My solution

- `display:flex` has `justify-content` to setup space between items in row
- when there is only image in the a tag it is best to use `aria-label=""` attribute to mention the text of the image so that screen reader can read it, `aria-label="twitter"`
- `display:inline-block` uses whole width in grid layout to fix it we can use `align-self:center/end`, `align is top to bottom alignment` `justify` is column wise alignment
- css reset: `img{display:block}`
- use css hover and focus to {opacity:.8} so that it can show that is a actionable thing

# 0042.A word on class naming

- talked about css class naming convention
  - bem
  - compound naming
  - cubic
- naming convention is not a big issue, each naming convention solves a particular problem
- try to be open, and see if any convention is speaking to you, means they are making sense to you

## 0043.Overlooked fundamentals wrap up

- here he talks about practicing and learning and not binge watching it and not absorb the content

## 0044.The unknown fundamentals introduction

- introduction about week 2 modules
- unknown fundamentals where we may struggle

## 0045.Unknown fundamentals project 1 introduction

- here is a hero project to build which i could'nt build

## 0046.Teaching you how to fish

- talks about how to learn new things
- talks about, mdn- mozilla development network
- https://developer.mozilla.org/en-US/docs/Web/CSS
- also good for javascript

## 0047.Introduction to formatting contexts

- formatting context
  - Everything is box, boxes inside box
  - the behavior of boxes depend on the formatting context
  - Four formatting context
    - `block`, `inline`, `flex`, `grid`
  - there are specific rules how content flow or format
  - if we learn these rules we can be consistent and will predict the design

## 0048.Inline formatting context and anonymous boxes

- inline formatting context & anonymous boxes
- common used inline elements are -`SPAN, STRONG, EM, LINKS(<a></a>)`
- inline elements go next to one another
- inline elements have some limitation
- other inline elements `<a><abbr><acronym><b><bdo><big><br><button><cite><code><dfn><em><i><img><input><kbd><label><map><object><output><q><samp><script><select><small><span><strong><sub><sup><textarea><time><tt><var>`
- In a horizontal writing mode, margins and padding, above and below the element will not be applied.
- When we have a block level element, it can either contain other block elements, or inline elements. it cannot contain a mix of them.
- example

  ```html
  <div>
    sentence 1
    <p>sentence 2</p>

    sentence 3
  </div>
  ```

  - all sentence 1,2,3 are block level element, and sentence 1 and 3 are anonymous element, this is done by the browser under the hood, we don't have any control over it

## 0049.Block formatting context

- Default html context

  - Boxes are laid out one on top of each other. Even if there is room, they won't try to squeeze in.  
    ![1](./images/49/1.jpg) ![2](images/49/2.jpg)
  - Margin between elements collapse  
    ![3](images/49/3.jpg) ![4](images/49/4.jpg) ![5](images/49/5.jpg) ![6](images/49/6.jpg) ![7](images/49/7.jpg)
  - And even move the parent element  
    ![8](images/49/8.jpg)

- A BFC as like a mini layout inside your page. Once an element creates a BFC

  - Everything is contained inside it.
  - Excludes all externally floated elements
  - Stop margin collapsing
  - Example

    - Without bfc the margin-top of first paragraph and margin-bottom of last paragraph is collapsed,but with bfc it includes the margin.  
      ![9](images/49/9.jpg)
    - It also makes the floating text block element  
      ![10](images/49/10.jpg)

- The root of our document (the html element) creates a block formatting context, which all of our content lives inside
- We can create new block formatting contexts within our document as well.
- You can create a new block formatting context in a lot of ways (this is just a few)
  - Using `float`
  - `position` is `abosolute` , `fixed` , or `inline-block`
  - `overflow` of anything except visible
  - Using `columns`
  - Flex and grid items
  - `display: flow-root`
- Note: with so many things creating a new formatting context, and because a new block formatting context stops margins from collapsing, it can be hard to be consistent

## 0050.Formatting context and floats

- example of previous lesson

## 0051.Collapsing margins in action

- in 45.0045.Unknown fundamentals project 1 introduction folder, we updated the hero code by fixing the margin collapse
- if the parent and the child are in same position then the margin collapse happen and parent move with child
- adding padding to parent will break this situation

## 0052.Creating a new formatting context

- solving the problem using block formatting context
- we give the parent `columns:1` and removed the padding and added it to child margin
- with this solution the layout is dependent with child, that type of solution is discouraged by the teacher

## 0053.Flex and grid formatting contexts

- When we declare `display: flex` on an element, it establishes a flex formatting context
- While very similar to establishing a new block formatting context, there are a few differences:
  - `float` and `clear` don't work
  - It's margins do not collapse with it's children's margins
  - The children are part of a flex layout, not a
    box layout
  - The children (flex items), establish their own
    formatting context, means children of flex items does not have the flex formatting contexts
- ### grid formatting context is same as flex formatting context, but different layout
- [example code-pen](https://codepen.io/kevinpowell/pen/11c167c4d7265c9414c3a45904cb2c16)

## 0054.Consistency

- The reason collapsing margins have inconsistency that text element and some other elements have default `margin-top` and `margin-bottom`
- one of the solution is reset

  - some people use below code to reset the default spacing

    ```css
    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
    }
    ```

  - there is a problem with this approach, it will also reset some of the defaults that can be useful, like the ul and li when we are using it to show the bullet with padding.
  - To solve the problem we can do a selective reset
  - example

  ```css
  h1,
  h2,
  h3,
  h4,
  p {
    margin: 0;
  }
  ul[class] {
    margin: 0;
    padding: 0;
    list-style: none;
  }
  ```

  - some time we want everything should behave like regular flow, there are two way to achieve that

  ```css
  /*method:1*/
  .flow-content > * {
    margin-bottom: 1rem;
  }
  .flow-content > *:last-child {
    margin-bottom: 0;
  }
  /*method:2*/
  .flow-content > * + * {
    margin-top: 1rem;
  }
  ```

- [code-pen example](https://codepen.io/kevinpowell/pen/83fa8fbdf17588511de97f74a4c326fe)

## 0055.Creating a css rule for flow content consistency

- ### Some fonts can give extra top and bottom gap without any margin or padding
- [code-pen example](https://codepen.io/kevinpowell/pen/83fa8fbdf17588511de97f74a4c326fe)
- demonstrate more on flow-content reset
- we want the grid and the flex flow content to not give the extra space to make it like normal flow text
- `.flow-content > *` all direct child of flow-control
- `.flow-content > *:last-child` save as above but if only is the last child
- `.flow-content > * + *` all direct child of flow-control and has a sibling before it
- we only want to use it where we need it

## 0056.Adding consistency to our magic page

Copy the magic in the air
Added reset

```css
h1,
h2,
h3,
p {
  margin: 0;
}
a {
  display: inline-block;
}
```

Added utility class

```css
.flow-content > * + * {
  margin-top: 1rem;
}
```

All this reset will solve the inconsistency, ie: the padding of hero_content become consistent

## 0057.Magic page finishing touches

Added style to button
Updated margin-top of flow-content
fixed missing style of h2 heading with span

## 0058.A look at the updated design

Completed the exercise, cheated little bit. Join section is left unfinished, overall good

## 0059.Easy wins

Mobile first design- design for mobile first
Then plan what style can be used multiple times and use them in utility class mean common designs
container padding given from variable

## 0060.Adding columns

Added responsive split utility class, which on small column and row on bigger screen

## 0061.The square corner decorations

Added before element, remember to use it without space like `.join-now li::before`, otherwise it will select all the children.
fixed margin reset of ul
added background to cta class

## 0062.Stepping up our spacing utility

Using the spacing variable we can set a default flow-content spacing and increase it with a modifier

# 10.Unknown Fundamentals - Stacking Context & Containing Blocks

## 0063.Stacking context and containing blocks introduction

Stacking context and containing blocks are related
