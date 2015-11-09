## Website Performance Optimization Project
#### Submitted by Nidhi Varma

### About the Website

On the website Cam's Pizzeria a person can choose pizza from hundreds of choices. There is something for everyone.

On this website you can
* Browse through the menu
* Choose the size of the pizza
* Make a choice of a speciality pizza
* Look at the locations we are serving

You cannot contact them because they are a virtual pizzeria.

### Optimizations

####Part 1: Optimize PageSpeed Insights score for index.html

1. Added "async" attribute to analytics.js
2. Added media = print attribute to print.css
3. Inlined the file perfmatters.js in index.html
4. Optimized the image pizzeria.jpg
5. Optimized and minified the style.css, and print.css

####Part 2: Optimize PageSpeed Insights score for pizzeria.html
1. Minified all css files
2. Compressed all the images
3. The main.js was not minified as the comments that were added needs to be readable by the reviewers
4. Added Viewport and increased the gap between the buttons (to enhance the PageSpeed score)

####Part 3: Optimizations performed to achieve 60 fps when scrolling pizzeria.html

Earlier in the function updatePositions(), phase was being calculated inside the for loop. Phases were repeating after every fifth term. So I realized that calculating phases inside the for loop which is going through items.length time is very expensive and needs to be out of that loop. I created an array with five elements. Then in a for loop of length five I calculated the phases and stored in an array. In the second for loop which iterates through all the elements, I calculated only style.left value using the five pre-calculated phases. This change alone helped achieve the 60 fps frame-rate when scrolling.

####Part 4: Optimizations performed to the function for resizing pizza

Earlier in the function "changePizzaSizes(size)" calculation of dx and newwidth was done inside the for loop for all the *div* elements of class *randomPizzaContainer*. As a result of that layout was called every time we were going through a loop. I realized that dx and newwidth values were same for all the div elements, and hence it can be done once outside the loop for one of the elements.

While the above optimization reduced the time from 99 msec to about 6 msec, it was still above the required time of 5 msec. I realized that the repeated call to document.querySelectorAll() was unnecessary. It would be pretty expensive to search through the document again and again for elements of class *randomPizzaContainer*. So I defined a temporary variable called *pizzaContainers* to store the array returned by the call to document.querySelectorAll(). After this change the time to execute the loop dropped down to less than 2 msec.
