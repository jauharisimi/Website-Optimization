## Website Performance Optimization portfolio project

This is my fourth project for Udacity Frontend Nanodegree Program. The purpose of this project is to teach how to optimize any site so that it loads as quickly as possible and runs at 60fps or faster.		I used Chrome developer tools to identify and fix performance issues(from nop-optimized images to poorly written Javascript to render-blocking CSS). 
I used Gulp a task runner for automated image optimization and minimization of HTML,CSS and uglify JS. 
For checking Page speed I used Page Speed Insights from Google Developer and used ngrok which allows us to create a tunnel from our local machine and input our .html files from our local computer out into the website.

Steps to ngrok:

1. you can run a local server

  ```bash
  $> cd /path/to/your-project-folder
  $> python -m SimpleHTTPServer 8080
  ```
2. Open a browser and visit localhost:8080
3.Download and install [ngrok](https://ngrok.com/) to make your local server accessible remotely.

  ``` bash
  $> cd /path/to/your-project-folder
  $> ngrok http 8080
  ```
4. Copy the public URL ngrok gives you and try running it through PageSpeed Insights.

### Getting started

The project contains the following files:
-dist (containing production code)
 	-css
 		-bootstrap-grid.css
		-print.css
		-style.css
		-style_pizzeria.css	
 	-img
 	-js
 		-main.js
 		-perfmatters.js
 	-index.html
 	-pizza.html
 	-project-2048.html
 	-project-mobile.html
 	-project-webperf.html
-src(containing source code)
	-css
		-bootstrap-grid.css
		-print.css
		-style.css
		-style_pizzeria.css	
 	-img
 	-js
 		-main.js
 		-perfmatters.js
 	-index.html
 	-pizza.html
 	-project-2048.html
 	-project-mobile.html
 	-project-webperf.htm
-gulpfile.js
-package.json
-README.md file.


####Part 1: Optimize PageSpeed Insights score for index.html
For optimizing the Page Speed for index.html:
1. Inline style.css 
2. Add media query to print.css
3. Async google-analytics script
4. Use Web Font loader to load the Google webfont asyncronously
5. Reduce the size of pizzaria.jpg to 100px width
6. Stored the images locally.
7. Used Gulp to: Minify CSS, HTML; Uglify JS; Compress jpg and png files and they are in dist folder.


####Part 2: Optimize Frames per Second in pizza.html and time to resize pizzas in less than 5 ms in pizza.html

Inorder to optimize pizza.html, we were required to modify js/main.js until our frames per second rate is 60 fps or higher. Following changes were made in the js/main.js file:

1. Replace all document.querySelector by document.getElementById. The querySelector and querySelectorAll lack the performance of their closely related functions: getElementById, getElementsByTagName, and getElementsByClassName. Both getElementsByTagName and getElementsByClassName return a DynamicNodeList, meaning it is live and changes to the DOM will be automatically reflected in the collection. Conversely, querySelectorAll returns a StaticNodeList that serves as a snapshot of the DOM unaffected by changes. Static node lists must collect the matched elements up-front while live node lists do not. It is these pre-computations that directly attribute to the degradation in performance of querySelectorAll.

2. Made some changes in function changePizzaSizes ---
a)Instead of calculating newWidth with value of dx and also use determineDx and offsetWidth which takes up long time, just used switch statement to assign the pizza size to newWidth and change the slider value to percent width.
b) Moved Variable PizzasDiv outside the FOR loop so as to avoid multiple DOM call.

3. Made some changes in function updatePositions ---
a) Assigned the value of scrollTop to variable scrollUp outside the loop to avoid carrying out layout multiple times.
b) Declared the variable phase outside the loop.Thus moved all the constants out of the FOR loop.
c) Stored values from for loop in pizzaArray.
d) Used transform property for visual formatting of pizza and also used translateX() to move the pizzas horizontally on the plane bcoz basic.left property takes large time to paint each frame.Inorder to make it work made some changes in .mover class in CSS too.

4. Added will-change property and transform: translateZ(0) property in CSS to .mover class. This property optimizes animations by letting the browser know which properties and elements are just about to be manipulated, potentially increasing the performance of that particular operation.

5. Added backface-visibility property to hidden in CSS to .mover class. This property defines whether or not an element should be visible when not facing the screen. So it is useful when an element is rotated ( like in our case background pizzas), and you do not want to see its backside.

6. Made some changes in document.addEventListener('DOMContentLoaded', function()) ---
a) Added code to calculate number of pizzas based on the viewport height of the user's screen instead of the originally set to 200. This reduces the time used in the creation of unnecessary pizza.
b) Moved the window.items = document.getElementsByClassName('mover') statement into this function inorder to stop updatePositions from re-defining items on every scroll event

You might find the FPS Counter/HUD Display useful in Chrome developer tools described here: [Chrome Dev Tools tips-and-tricks](https://developer.chrome.com/devtools/docs/tips-and-tricks).

### Optimization Tips and Tricks
* [Optimizing Performance](https://developers.google.com/web/fundamentals/performance/ "web performance")
* [Analyzing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/analyzing-crp.html "analyzing crp")
* [Optimizing the Critical Rendering Path](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/optimizing-critical-rendering-path.html "optimize the crp!")
* [Avoiding Rendering Blocking CSS](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/render-blocking-css.html "render blocking css")
* [Optimizing JavaScript](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/adding-interactivity-with-javascript.html "javascript")
* [Measuring with Navigation Timing](https://developers.google.com/web/fundamentals/performance/critical-rendering-path/measure-crp.html "nav timing api"). We didn't cover the Navigation Timing API in the first two lessons but it's an incredibly useful tool for automated page profiling. I highly recommend reading.
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/eliminate-downloads.html">The fewer the downloads, the better</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/optimize-encoding-and-transfer.html">Reduce the size of text</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/image-optimization.html">Optimize images</a>
* <a href="https://developers.google.com/web/fundamentals/performance/optimizing-content-efficiency/http-caching.html">HTTP caching</a>

### Customization with Bootstrap
The portfolio was built on Twitter's <a href="http://getbootstrap.com/">Bootstrap</a> framework. All custom styles are in `dist/css/portfolio.css` in the portfolio repo.

* <a href="http://getbootstrap.com/css/">Bootstrap's CSS Classes</a>
* <a href="http://getbootstrap.com/components/">Bootstrap's Components</a>

### Sample Portfolios

Feeling uninspired by the portfolio? Here's a list of cool portfolios I found after a few minutes of Googling.

* <a href="http://www.reddit.com/r/webdev/comments/280qkr/would_anybody_like_to_post_their_portfolio_site/">A great discussion about portfolios on reddit</a>
* <a href="http://ianlunn.co.uk/">http://ianlunn.co.uk/</a>
* <a href="http://www.adhamdannaway.com/portfolio">http://www.adhamdannaway.com/portfolio</a>
* <a href="http://www.timboelaars.nl/">http://www.timboelaars.nl/</a>
* <a href="http://futoryan.prosite.com/">http://futoryan.prosite.com/</a>
* <a href="http://playonpixels.prosite.com/21591/projects">http://playonpixels.prosite.com/21591/projects</a>
* <a href="http://colintrenter.prosite.com/">http://colintrenter.prosite.com/</a>
* <a href="http://calebmorris.prosite.com/">http://calebmorris.prosite.com/</a>
* <a href="http://www.cullywright.com/">http://www.cullywright.com/</a>
* <a href="http://yourjustlucky.com/">http://yourjustlucky.com/</a>
* <a href="http://nicoledominguez.com/portfolio/">http://nicoledominguez.com/portfolio/</a>
* <a href="http://www.roxannecook.com/">http://www.roxannecook.com/</a>
* <a href="http://www.84colors.com/portfolio.html">http://www.84colors.com/portfolio.html</a>
