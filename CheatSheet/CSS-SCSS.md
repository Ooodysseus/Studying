# CSS & SCSS Cheatsheet

## Selectors
* {}  
div {}  
.class {}  
#id {}  
a:hover {}  
ul > li {}  
input:focus {}  
p:first-child {}  
li:last-child {}  
:nth-child(2n) {}  
[class^="icon"] {}  
[data-attr] {}  
button:disabled {}  
a:active {}  
h1, h2, h3 {}  

## Properties
color: #333;  
background: #fff;  
margin: 10px;  
padding: 20px;  
border: 1px solid #ccc;  
border-radius: 5px;  
box-shadow: 0 2px 8px #0003;  
width: 100px;  
height: 50px;  
max-width: 100%;  
min-height: 100vh;  
font-size: 16px;  
font-family: Arial, sans-serif;  
font-weight: bold;  
line-height: 1.4;  
text-align: center;  
text-decoration: none;  
letter-spacing: 0.05em;  
word-break: break-all;  
overflow: hidden;  
overflow-y: scroll;  
display: block;  
display: flex;  
display: grid;  
align-items: center;  
justify-content: space-between;  
gap: 1rem;  
flex-direction: column;  
flex-wrap: wrap;  
grid-template-columns: repeat(3, 1fr);  
grid-gap: 20px;  
position: relative;  
top: 10px;  
left: 20px;  
z-index: 10;  
cursor: pointer;  
transition: all 0.3s;  
animation: fadein 1s;  
opacity: 0.7;  
visibility: hidden;  
pointer-events: none;  
user-select: none;  
white-space: nowrap;  

## Pseudo Elements
::before  
::after  
::placeholder  
::selection  
.content::before { content: '• '; }  

## Media Queries
@media (max-width:600px) { body { font-size: 14px; } }  
@media (min-width:1200px) { .container { width: 1140px; } }  

## Variables (CSS)
:root { --main-color: #09f; }  
color: var(--main-color);  

## Custom Fonts
@font-face {  
  font-family: 'MyFont';  
  src: url('myfont.woff2') format('woff2');  
}  
body { font-family: 'MyFont', sans-serif; }  

## Keyframes
@keyframes fadein {  
  from { opacity: 0; }  
  to { opacity: 1; }  
}  
.fadein { animation: fadein 2s; }  

## Responsive
img { width: 100%; height: auto; }  
.container { max-width: 1200px; margin: 0 auto; }  
.hide-mobile { display: none; }  
@media (min-width: 768px) { .hide-mobile { display: block; } }  

## Reset
* { margin: 0; padding: 0; box-sizing: border-box; }  

## Flexbox
display: flex;  
flex-direction: row;  
flex-direction: column;  
justify-content: center;  
align-items: flex-end;  
flex-wrap: wrap;  
gap: 20px;  
flex: 1 1 200px;  
.order-1 { order: 1; }  

## Grid
display: grid;  
grid-template-columns: repeat(3, 1fr);  
grid-column-gap: 10px;  
grid-row-gap: 20px;  
grid-area: header;  
.item { grid-column: 2 / 4; }  
.grid { grid-template-areas: "header header" "side main"; }  

## Transitions & Animations
transition: background 0.2s;  
transition: all 0.3s ease;  
animation: bounce 1s infinite;  

## Shadows
box-shadow: 0 2px 8px #0002;  
text-shadow: 1px 1px 2px #0005;  

## Border
border: 1px solid #333;  
border-radius: 50%;  
border-bottom: 2px dashed #f00;  

## List Styling
ul { list-style: none; }  
li { margin-bottom: 8px; }  
ol { padding-left: 2em; }  
li::marker { color: #09f; }  

## Buttons
button {  
  background: #09f;  
  color: #fff;  
  border: none;  
  border-radius: 4px;  
  padding: 0.5em 1em;  
  cursor: pointer;  
  transition: background 0.2s;  
}  
button:hover { background: #0077cc; }  
button:active { background: #005fa3; }  
button:disabled { opacity: 0.5; cursor: not-allowed; }  

## Forms
input, textarea, select {  
  border: 1px solid #ccc;  
  border-radius: 3px;  
  padding: 0.5em;  
  font-size: 1em;  
}  
input:focus { border-color: #09f; outline: none; }  
label { display: block; margin-bottom: 0.3em; }  

## Images
img { max-width: 100%; height: auto; border-radius: 8px; }  
.avatar { width: 40px; height: 40px; border-radius: 50%; }  

## Utility Classes
.text-center { text-align: center; }  
.text-right { text-align: right; }  
.mt-1 { margin-top: 1rem; }  
.mb-2 { margin-bottom: 2rem; }  
.p-2 { padding: 2rem; }  
.d-none { display: none; }  
.d-block { display: block; }  
.flex { display: flex; }  
.grid { display: grid; }  
.w-100 { width: 100%; }  
.h-100 { height: 100%; }  
.rounded { border-radius: 8px; }  

## Accessibility
[aria-label="Close"]  
button:focus { outline: 2px solid #09f; }  

## SCSS Variables
$main-color: #09f;  
$radius: 5px;  
$font-stack: Arial, sans-serif;  

## SCSS Nesting
nav {  
  ul {  
    li {  
      a { color: $main-color; }  
    }  
  }  
}  

## SCSS Mixins
@mixin center-flex {  
  display: flex;  
  align-items: center;  
  justify-content: center;  
}  
.box { @include center-flex; }  

## SCSS Functions
@function px-to-rem($px, $base: 16) {  
  @return ($px / $base) * 1rem;  
}  
h1 { font-size: px-to-rem(32); }  

## SCSS Extends
%btn {  
  padding: 0.5em 1em;  
  border-radius: $radius;  
}  
.button { @extend %btn; }  

## SCSS Operators
width: 100% - 20px;  
padding: $base-padding * 2;  

## SCSS Imports
@import 'variables';  
@import 'mixins';  
@import 'base/reset';  

## SCSS Conditionals
@if $main-color == #09f {  
  background: #fff;  
}  
@else {  
  background: #222;  
}  

## SCSS Loops
@for $i from 1 through 5 {  
  .m-#{$i} { margin: $i * 4px; }  
}  
@each $color in red, green, blue {  
  .text-#{$color} { color: $color; }  
}  

## SCSS Maps
$colors: (  
  primary: #09f,  
  secondary: #f90,  
  error: #f00  
);  
.btn-primary { background: map-get($colors, primary); }  

## Important
!important  

## Comments
/* CSS comment */  
// SCSS comment  

## Best Practices
Use variables for colors  
Group common styles  
Use rem/em for font sizes  
Reset browser styles  
Use utility classes  
Minimize !important usage  
Use flex/grid for layout  
Test responsive design  
Organize SCSS files by feature  
Comment complex logic  
Avoid deep nesting  
Leverage mixins for reuse  
Use media queries for breakpoints  
Use semantic HTML markup  
Optimize for accessibility  
Use CSS custom properties for theme  
Compress output for production  
Prefer shorthand properties  
Use transition for smooth effects  
Use box-sizing: border-box  
Keep specificity low  
Limit global styles  
Manage color palette via variables  
Use consistent naming conventions  
Modularize stylesheets  
Avoid inline styles  
Minimize selector length  
Avoid large CSS files  
Remove unused styles  
Prefer BEM for class names  
Test in multiple browsers  
Use preprocessor for scaling  
Organize variables and mixins  
Use partials for imports  
Document style decisions  
Keep animations performant  
Minimize repaint/reflow  
Use hardware-accelerated props  
Be careful with z-index stacking  
Prefer CSS Grid for complex layouts  
Use fallback fonts  
Set base font size  
Test dark and light themes  
Support high-contrast mode  
Use high-res images  
Minimize HTTP requests  
Avoid CSS hacks  
Validate CSS  
Lint styles  
Use autoprefixer  
Version your styles  
Keep dependencies updated  
Consider CSS frameworks  
Prefer semantic units  
Use responsive images  
Handle SVG styling  
Use logical properties  
Test print media  
Minimize specificity wars  
Keep code readable  
Name classes meaningfully  
Document theme structure  
Use consistent spacing  
Optimize for performance  
Avoid !important except utility  
Avoid global resets in components  
Minimize use of floats  
Prefer flex over float  
Test in mobile emulators  
Support accessibility standards  
Set touch targets  
Use ARIA roles  
Hide elements accessibly  
Use visually-hidden for a11y  
Test color contrast  
Support high DPI screens  
Use CSS variables for theming  
Document breakpoints  
Keep code modular  
Organize selectors by context  
Use layer system for z-index  
Prefer CSS over JS for animation  
Test fallback for features  
Support legacy gracefully  
Comment browser hacks  
Avoid over-specific selectors  
Keep selectors flat  
Minimize overrides  
Use CSS logical props  
Compress production builds  
Test with screen readers  
Avoid magic numbers  
Keep custom properties scoped  
Version theme files  
Use CSS-in-JS if needed  
Prefer modular CSS  
Document naming conventions  
Test with real users  
