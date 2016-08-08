---
layout: lesson
title: "News reader effects"
desc: "Use CSS effects like transitions and animations to make a simple news reader interface."

video: "4bOwe1_gfS8"

extra_tutorials:
  - title: "CSS animations & effects"
    url: css-animations-effects
  - title: "CSS effects slide deck"
    url: /courses/web-dev-4/css-effects/

goal:
  before: |
    We’re going to look at how to use `transform`, `transition`, `animation` and `:target` while creating a mock news reader.

    The red diamond badge should pulse. Clicking on each tab should display a different thing on the screen.
  notes:
    - label: "Type it, type it real good"
      text: "Remember the purpose of this lesson is to type the code out yourself—build up that muscle memory in your fingers!"

steps:
  - title: "Set up project"
    before: |
      Before we get started, create some files and get ready.

      1. Create a folder named `news-reader`
      2. Make an `index.html` & add the boilerplate code.
      4. Make a `main.css` in your `css` folder & add the boilerplate code.
    notes:
      - label: "Naming conventions"
        text: "Don’t forget to follow the [naming conventions](/topics/naming-paths-cheat-sheet/#naming-conventions)."
      - label: "HTML snippets"
        text: "Create the boilerplate with `html5`, `viewport`, `css`"
      - label: "CSS snippets"
        text: "Create the boilerplate with `cssviewport`, `borderbox`, `textsize`"

  - title: "Write the HTML"
    before: |
      Here’s the HTML we need to make the news reader interface.
    code_lang: "html"
    code_file: "index.html"
    code: |
      ⋮
      <ul class="tabs">
        <li><a href="#sci-fi">Sci-fi</a></li>
        <li><a href="#dinos"><i class="badge"></i>Dinosaurs!</a></li>
        <li><a href="#space">Space</a></li>
      </ul>

      <div class="panel" id="sci-fi">
        <h2>Sci-Fi</h2>
      </div>

      <div class="panel" id="dinos">
        <h2>Dinosaurs!</h2>
      </div>

      <div class="panel" id="space">
        <h2>Space</h2>
      </div>
      ⋮
    lines:
      - num: 3
        text: "The `<a>` tags link to the `id` of panels further down the page, for use with CSS `:target`"
      - num: 4
        text: "Using an `<i>` tag for the pulsing badge—it’s semantically okay because there’s no content inside."
      - num: 8
        text: "Each `.panel` has a unique `id` so that `:target` can work."

  - title: "Write the CSS"
    before: |
      Here’s the CSS we need to make the news reader interface.
    code_lang: "css"
    code_file: "css/main.css"
    code: |
      ⋮
      .tabs {
        margin: 0;
        padding: 0;
        list-style-type: none;
      }

      .tabs > li {
        display: inline-block;
      }

      .tabs a {
        display: inline-block;
        background-color: #e2e2e2;
        color: #000;
        text-decoration: none;
        padding: .5em .75em;
        border-radius: 8px;
        transition: all 500ms linear;
        position: relative;
      }

      .tabs a:hover {
        background-color: #000;
        color: #fff;
      }

      .badge {
        position: absolute;
        width: 10px;
        height: 10px;
        background-color: red;
        top: -5px;
        left: calc(50% - 5px);
        transform: rotate(45deg);
        animation: pulse 1s linear infinite alternate;
      }

      @keyframes pulse {
        0% {
          opacity: .2;
          transform: scale(.7) rotate(45deg);
        }
        100% {
          opacity: 1;
          transform: scale(1) rotate(45deg);
        }
      }

      .panel {
        display: none;
      }

      .panel:target {
        display: block;
      }
    lines:
      - num: 19
        text: |
          The `transition` is always on the default state—not where the properties change.
          - `all` — animate all the CSS properties that change.
          - `500ms` — the duration of the animation.
          - `linear` — the easing; `linear` means no easing.
      - num: "23-26"
        text: "Change a few CSS properties when the element is hovered. Only properties that are numbers can be transitioned. When the element is interacted with the transition will occur."
      - num: 34
        text: |
          Use `calc()` to perfectly centre the element. Because its `left` is `50%`, it isn’t perfectly centred—its left edge is at the centre.

          So, using `calc()` we bump it back by half its width—making it perfectly centred.
      - num: 35
        text: "Use `transform` to rotate the `<i>` tag so it visually looks like a diamond."
      - num: 36
        text: |
          Add an automatically playing `animation` to the badge.
          - `pulse` — the name of the keyframes to use.
          - `1s` — the duration of the animation; could also be specified in `ms`
          - `linear` — the easing; `linear` means no easing.
          - `infinite` — how many times the animation should play; could be just a number.
          - `alternate` — tells the animation to play forward through the keyframes, then backward.
      - num: "39-48"
        text: |
          The keyframes block of an animation. All keyframe blocks need to be given a name.

          Keyframes are specified in percent so they aren’t tied to a specific duration. There can be as many percentage-based keyframes as you want—including decimals like `57.4%`

          Within each keyframe we only need to specify the CSS properties that are going to change. Any property that is a number can be animated.
      - num: "54-56"
        text: |
          By default the `.panel` is hidden (shown in the CSS above).

          When it’s `id` is found in the URL, aka it’s the target, add this CSS to it. So, when `.panel` is targetted it becomes visible with `display: block`

---