# HTML Cheatsheet

## Basic Structure
<!DOCTYPE html>  
<html>  
  <head>  
    <title>Page Title</title>  
    <meta charset="UTF-8">  
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  
  </head>  
  <body>  
    <!-- Content here -->  
  </body>  
</html>  

## Head Elements
<title>Title</title>  
<meta name="description" content="Cheatsheet">  
<link rel="stylesheet" href="style.css">  
<script src="script.js"></script>  
<meta name="author" content="Ooodysseus">  
<meta property="og:title" content="HTML Cheatsheet">  
<base href="/">  

## Text Elements
<h1>Heading 1</h1>  
<h2>Heading 2</h2>  
<h3>Heading 3</h3>  
<p>Paragraph text</p>  
<span>Inline text</span>  
<strong>Strong</strong>  
<em>Emphasized</em>  
<b>Bold</b>  
<i>Italic</i>  
<u>Underline</u>  
<mark>Highlight</mark>  
<small>Small</small>  
<del>Deleted</del>  
<abbr title="HyperText Markup Language">HTML</abbr>  
<blockquote cite="https://example.com">Quote</blockquote>  
<code>Inline code</code>  
<pre>Preformatted  
  text</pre>  

## Links
<a href="https://example.com">Link</a>  
<a href="mailto:mail@example.com">Email</a>  
<a href="#section">Anchor</a>  
<a href="tel:+1234567890">Call</a>  
<a href="file.pdf" download>Download</a>  
<a href="https://example.com" target="_blank" rel="noopener">External</a>  

## Lists
<ul>  
  <li>Item 1</li>  
  <li>Item 2</li>  
</ul>  
<ol>  
  <li>First</li>  
  <li>Second</li>  
</ol>  
<dl>  
  <dt>Term</dt>  
  <dd>Definition</dd>  
</dl>  

## Images
<img src="image.jpg" alt="Description">  
<img src="icon.svg" width="32" height="32">  
<picture>  
  <source srcset="image.webp" type="image/webp">  
  <img src="image.jpg" alt="Fallback">  
</picture>  
<figure>  
  <img src="pic.jpg" alt="Pic">  
  <figcaption>Caption</figcaption>  
</figure>  

## Audio/Video
<audio src="audio.mp3" controls></audio>  
<video src="video.mp4" controls width="320"></video>  
<source src="movie.mp4" type="video/mp4">  
<track src="subtitles.vtt" kind="subtitles" srclang="en" label="English">  

## Tables
<table>  
  <caption>Description</caption>  
  <thead>  
    <tr><th>Header</th></tr>  
  </thead>  
  <tbody>  
    <tr><td>Data</td></tr>  
  </tbody>  
  <tfoot>  
    <tr><td>Footer</td></tr>  
  </tfoot>  
</table>  

## Forms
<form action="/submit" method="post">  
  <input type="text" name="name" required>  
  <input type="email" name="email">  
  <input type="password" name="pass">  
  <input type="file" name="file">  
  <input type="checkbox" name="subscribe" checked>  
  <input type="radio" name="gender" value="male">  
  <input type="range" min="0" max="10">  
  <input type="color" value="#ff0000">  
  <input type="date">  
  <select name="country">  
    <option value="ua">Ukraine</option>  
    <option value="us">USA</option>  
  </select>  
  <textarea name="comment"></textarea>  
  <button type="submit">Send</button>  
  <button type="reset">Reset</button>  
</form>  

## Form Attributes
<input disabled>  
<input readonly>  
<input required>  
<input autofocus>  
<input placeholder="Type here">  
<input minlength="4" maxlength="16">  
<input pattern="[A-Za-z]{3,}">  
<input autocomplete="on">  
<form novalidate>  

## Semantic Elements
<header>Header</header>  
<nav>Navigation</nav>  
<main>Main content</main>  
<aside>Sidebar</aside>  
<section>Section</section>  
<article>Article</article>  
<footer>Footer</footer>  
<details>  
  <summary>Show More</summary>  
  Details hidden  
</details>  
<time datetime="2025-08-01">Aug 1, 2025</time>  
<meter value="0.6">60%</meter>  
<progress value="40" max="100"></progress>  
<address>Kyiv, Ukraine</address>  

## Input Types
text  
email  
password  
number  
date  
datetime-local  
month  
week  
time  
search  
tel  
url  
color  
range  
checkbox  
radio  
file  
hidden  

## Button Types
<button type="button">Button</button>  
<button type="submit">Submit</button>  
<button type="reset">Reset</button>  
<input type="button" value="Input Button">  

## SVG
<svg width="100" height="100">  
  <circle cx="50" cy="50" r="40" fill="red" />  
</svg>  

## Canvas
<canvas id="myCanvas" width="200" height="100"></canvas>  

## Embedded Content
<iframe src="https://example.com"></iframe>  
<embed src="file.swf">  
<object data="file.pdf" type="application/pdf"></object>  
<template>Hidden markup</template>  

## Accessibility
<img alt="Description">  
<label for="input">Label</label>  
<input id="input">  
<fieldset>  
  <legend>Description</legend>  
</fieldset>  
<aria-label="Close">  
<tabindex="0">  
<role="button">  

## Meta Tags
<meta name="viewport" content="width=device-width,initial-scale=1.0">  
<meta http-equiv="X-UA-Compatible" content="IE=edge">  
<meta name="theme-color" content="#09f">  

## Favicons
<link rel="icon" href="favicon.ico">  
<link rel="apple-touch-icon" href="apple-touch-icon.png">  

## Scripting
<script src="script.js"></script>  
<script>console.log('Hello')</script>  
<script type="module" src="main.mjs"></script>  
<noscript>Please enable JS</noscript>  

## Styles
<link rel="stylesheet" href="style.css">  
<style>body { background: #eee; }</style>  

## Data Attributes
<div data-user-id="123"></div>  
<input data-action="save">  
document.querySelector('[data-user-id]')  

## Miscellaneous
<hr>  
<br>  
<wbr>  
<sup>2</sup>  
<sub>2</sub>  
<kbd>Ctrl+C</kbd>  
<samp>Sample output</samp>  
<var>x</var>  
<dfn>Definition</dfn>  
<ruby>漢 <rt>Kan</rt></ruby>  
<output id="result"></output>  

## Comments
<!-- HTML comment -->  

## Best Practices
Use semantic tags  
Add alt to images  
Keep markup readable  
Indent nested elements  
Use labels for inputs  
Set page charset and viewport  
Minimize inline styles/scripts  
Avoid unnecessary divs  
Validate HTML  
Use external CSS/JS  
Optimize images  
Test accessibility  
Support responsive design  
Set lang attribute  
Keep forms accessible  
Use unique IDs  
Limit use of tables for layout  
Use ARIA roles for a11y  
Prefer <button> over <input type="button">  
Group form fields with <fieldset>  
Use <main> for main content  
Set favicon  
Use heading hierarchy  
Avoid obsolete tags  
Use <template> for hidden markup  
Document structure  
Minimize global attributes  
Test on multiple browsers  
Compress images  
Limit <iframe> usage  
Use <svg> for vector graphics  
Use <canvas> for drawing  
Use meta description  
Support dark mode  
Use lazy loading for images  
Optimize for SEO  
Prefer user-friendly URLs  
Support keyboard navigation  
Limit use of <br>  
Use rel="noopener" for external links  
Comment complex sections  
Test on mobile devices  
Ensure color contrast  
Use consistent naming  
Avoid inline event handlers  
Prefer <section> for logical grouping  
Keep forms simple  
Test file uploads  
Use <noscript> where needed  
Manage tab order  
Avoid duplicate IDs  
Support localization  
Use <address> for contact info  
Group navigation in <nav>  
Use <footer> for copyright  
Document form actions  
Validate user input  
Handle errors gracefully  
Support progressive enhancement  
Keep code DRY  
Organize files logically  
Review HTML5 updates  
Test accessibility tools  
Provide helpful feedback  
Version your templates  
Automate builds  
Use code linters  
Document APIs  
Set canonical URLs  
Minimize third-party scripts  
Monitor performance  
Backup files  
Keep structure modular  
Test edge cases  
Refactor old markup  
Archive unused pages  
Review dependencies  
Keep changelog  
Support new standards  
Comment intent  
Use modern HTML  
Prefer HTTPS  
Provide help/about pages  
Monitor analytics  
Test real-world scenarios  
