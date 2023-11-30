출처: “State of CSS” at Google IO 2022

https://io.google/2022/program/9f58d739-87b1-42f0-b715-32584508a69b/

출연자: Adam Argyle, Chrome Developer Relations Engineer at Google

The year 2022 is set to be one of CSS's greatest years, in both features and cooperative browser feature releases, with a collaborative goal to implement 14 features!

# @layer

- Feature: The **`@layer`** [CSS](https://developer.mozilla.org/en-US/docs/Web/CSS) [at-rule](https://developer.mozilla.org/en-US/docs/Web/CSS/At-rule) is used to declare a cascade layer and can also be used to define the order of precedence in case of multiple cascade layers.
- Syntax
  ```jsx
  @layer layer-name {rules}
  @layer layer-name;
  @layer layer-name, layer-name, layer-name;
  @layer {rules}
  ```
- Browser support:
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c457b2dc-042d-4b3e-97fb-1943f7316d9d/Untitled.png)
- Example
  https://interactive-examples.mdn.mozilla.net/pages/tabbed/at-rule-layer.html

# Subgrid

- Feature: Before `subgrid`, a grid inside of another grid couldn't align itself to its parent cells or grid lines. After `subgrid`, a child of a grid can adopt its parents’ columns or rows as its own, and align itself or children to them!
- Syntax:
  ```jsx
  .parent {
  	display: grid;
  	grid-template-columns
  	grid-template-rows
  }
  .child {
  	display: grid
  	grid-template-columns: subgrid;
  	grid-template-rows: subgrid;
  }
  ```
- Browser support:
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/28e978b0-5419-4ed3-80b1-4ca6de89467e/Untitled.png)
- Example:
  https://mdn.github.io/css-examples/grid/subgrid/columns.html

# @container

- Feature:
  Before `@container`, elements of a webpage could only respond to the size of the whole viewport. This is great for macro layouts, but for micro layouts, where their outer container isn't the whole viewport, it's impossible for the layout to adjust accordingly.
  After `@container`, elements can respond to a parent container size or style! The only caveat is the containers must declare themselves as possible query targets, which is a small requirement for a large benefit.
- Syntax:
  ```jsx
  .card {
    container-type: inline-size;
  }

  @container (max-width: 850px) {
    .links {
      display: none;
    }

    .time {
      font-size: 1.25rem;
    }
  }
  ```
- Browser support:
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0a011a73-b7ab-43a0-a9c0-7863f2008fa0/Untitled.png)
- Example:
  https://codepen.io/una/pen/LYbvKpK

# @accent-color

- Feature:
  Before `accent-color`, when you wanted a form with brand matching colors, you could end up with complex libraries or CSS solutions that became hard to manage over time. While they gave you all the options, and hopefully included accessibility, the choice to use the built-in components or adopt your own becomes tedious to continue to choose.
  After `accent-color`, one line of CSS brings a brand color to the built-in components. In addition to a tint, the browser intelligently chooses proper contrasting colors for ancillary parts of the component and adapts to system color schemes (light or dark).
- Syntax:
  ```jsx
  /* tint everything */
  :root {
    accent-color: hotpink;
  }

  /* tint one element */
  progress {
    accent-color: indigo;
  }
  ```
- Browser support:
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/74c09970-3dac-4f14-a695-67be39acd9d5/Untitled.png)
- Example:
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/57f743e3-195a-43e7-9657-79008c82dc22/Untitled.png)

# inert

- Feature: The `[HTMLElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement)` property **`inert`** reflects the value of the element's `[inert](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/inert)` attribute. It is a boolean value that, when present, makes the browser "ignore" **user input events for the element**, including focus events and events from assistive technologies. The browser may also ignore page search and text selection in the element.
- Syntax:
  ```jsx
  <div>
    <label for="button1">Button 1</label>
    <button id="button1">I am not inert</button>
  </div>
  <div inert>
    <label for="button2">Button 2</label>
    <button id="button2">I am inert</button>
  </div>

  [inert] > * {
    opacity: 0.5;
  }
  ```
- Browser support:
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4305b3c0-8552-4cd0-a625-cf1b614a5527/Untitled.png)
- Example:
  https://live-samples.mdn.mozilla.net/en-US/docs/Web/API/HTMLElement/inert/_sample_.example.html
  https://storage.googleapis.com/web-dev-uploads/video/vS06HQ1YTsbMKSFTIPl2iogUQP73/gjWn8LZ22HdGX8pGZgwv.mp4

# COLRv1 Fonts

- Feature: Supports this fonts
  smaller footprint, vector-scalable, repositionable, gradient-featuring, and blend-mode powered fonts that accept parameters to customize the font per use case or to match a brand
- Syntax:
  ```jsx
  @import url(https://fonts.googleapis.com/css2?family=Bungee+Spice);

  @font-palette-values --colorized {
    font-family: "Bungee Spice";
    base-palette: 0;
    override-colors: 0 hotpink, 1 cyan, 2 white;
  }
  ```
- Browser support:
- Example:
  https://codepen.io/_rahul/pen/yLqGwqW
  https://glitch.com/embed/#!/embed/colrv1-emoji-vs-cbdt?attributionHidden=true&sidebarCollapsed=true&path=index.html&previewSize=100

# Viewport units

- Feature:
- Syntax:
  ```jsx
  Height: vh, dvh, svh, lvh;
  Block: vb, dvb, svb, lvb;
  Width: vw, dvw, svw, lvw;
  inline: vi, dvi, svi, lvi;
  ```
- Browser support:
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a3e1f219-833e-4609-83f0-7effab9ba8de/Untitled.png)
- Example:
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/de5d9570-6a79-4839-8ac1-b9f3cb83b640/Untitled.png)

# :has()

- Feature:
  Before `:has()`, the [subject](https://developer.mozilla.org/docs/Learn/CSS/Building_blocks/Selectors#:~:text=The%20element%20or%20elements%20which%20are%20selected%20by%20the%20selector%20are%20referred%20to%20as%20the%20subject%20of%20the%20selector.) of a [selector](https://web.dev/learn/css/selectors/) was always at the end.
  After `:has()`, a subject higher in the element tree can remain the subject while providing a query about children:
- Syntax:
  ```jsx
  .parent:has(.child) {...}
  section:has(*:focus-visible) {...}
  a:has(> img) {...}
  ```
- Browser support:
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/fd5d9be7-76e8-46c6-b98a-b00e7175b3f8/Untitled.png)
- Example:
  ```jsx
  /* Matches <a> elements that contain an <img> child */
  a:has(img) { … }

  /* Matches <a> elements that directly contain an <img> child */
  a:has(> img) { … }

  /* Matches <section> elements that don’t contain any heading elements: */
  section:not(:has(h1, h2, h3, h4, h5, h6))
  ```

# Loosely typed custom properties

- Feature: The flexibility of CSS syntax makes animating some things impossible, such as gradients.
- Syntax:
  ```jsx
  @property --x {
    syntax: '<length>';
    initial-value: 0px;
    inherits: false;
  }
  ```
- Browser support:
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d1ec3eff-161a-40f5-a58f-c247ec5bc1ea/Untitled.png)
- Example:
  https://codepen.io/web-dot-dev/pen/RwxXVGx

# Media query ranges

- Feature: much more legible
- Syntax:
  ```jsx
  @media (320px <= width <= 1280px) {
    …
  }

  @media (width >= 320px) {
    …
  }
  ```
- Browser support:
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e672a4d0-34f1-4601-9109-7a717b253899/Untitled.png)
- Example:
  ```jsx
  # Before
  @media (min-width: 320px) and (max-width: 1280px) {
    …
  }

  # After
  @media (320px <= width <= 1280px) {
    …
  }
  ```

# @nest

- Feature: the repetition is gone
- Syntax:
  ```jsx
  & > child
  @nest selector
  ```
- Browser support:
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/dd9ff9a8-1599-48f6-8390-c99b0e9a4c90/Untitled.png)
- Example:
  ```jsx
  article {
    color: darkgray;
  }

  article > a {
    color: var(--link-color);
  }

  /* with @nest becomes */

  article {
    color: darkgray;

    & > a {
      color: var(--link-color);
    }
  }

  ######################################

  /* parent owns this, adjusting children */
  section:focus-within > article {
    border: 1px solid hotpink;
  }

  /* with @nest becomes */

  /* article owns this, adjusting itself when inside a section:focus-within */
  article {
    @nest section:focus-within > & {
       border: 1px solid hotpink;
    }
  }
  ```

# @scope

- Feature: styles are scoped to only within a context
- Syntax:
  ```jsx
  @scope (.card) {
    header {
      color: var(--text);
    }
  }
  ```
- Browser support:
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/7ad2b0d4-36f7-4e19-863f-e678d3114da5/Untitled.png)
- Example:
  ```jsx
  @scope (.light-theme) {
    a { color: purple; }
  }

  @scope (.dark-theme) {
    a { color: plum; }
  }
  ```

# Prefers-reduced-data media query

- Feature:
- Syntax:
  ```jsx
  @media (prefers-reduced-data: reduce) {
    picture, video {
      display: none;
    }
  }
  ```
- Browser support:
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/e68e7e0c-7ab0-400a-859e-b1c2a7b68d28/Untitled.png)
- Example:
  https://storage.googleapis.com/web-dev-uploads/video/vS06HQ1YTsbMKSFTIPl2iogUQP73/3Vwnp23TzTTBjFCan6oG.mp4

# Toggle()

- Feature: toggleable state with a DOM element
- Syntax:
  ```jsx
  html {
   toggle-root: mode [auto light dark];
  }

  html:toggle(mode light) {...}
  html:toggle(mode dark) { ...}

  .mode-btn {
  	toggle-trigger: mode;
  }
  ```
- Browser support:
- Example:

# anchor()

- Feature: can position elements to other elements
- Syntax:
  ```jsx
  <button id="myButton" popup="myPopup">Anchor</button>
  <popup id="myPopup" anchor="myButton">Anchored element</popup>
  ```
- Browser support:
- Example:
  ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/0fa7dffe-a945-43e1-b852-5f95c859111c/Untitled.png)
