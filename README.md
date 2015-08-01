## Website Performance Optimization portfolio project

### Running the application

The most efficient method for running the application is to open your web browser and navigate to http://jtrob704.github.io/frontend-nanodegree-mobile-portfolio/

You can also obtain the source from https://github.com/jtrob704/frontend-nanodegree-mobile-portfolio

### Optimizations to views/js/main.js

Based on code from Cameron Pittman's Browser Rendering Optimization Course. https://www.udacity.com/course/viewer#!/c-ud860-nd
Removed multiple queries to the DOM for the .randomPizzaContainer selector. Replaced with variable randomPizzas that holds the collection of DOM nodes.
Removed unnecessary determineDx function.

```javascript
function changePizzaSizes(size) {
        switch (size) {
            case "1":
                newWidth = 25;
                break;
            case "2":
                newWidth = 33.3;
                break;
            case "3":
                newWidth = 50;
                break;
            default:
                console.log("bug in sizeSwitcher");
        }

        var randomPizzas = document.querySelectorAll(".randomPizzaContainer");

        for (var i = 0; i < randomPizzas.length; i++) {
            randomPizzas[i].style.width = newWidth + "%";
        }
    }
```

 Removed scrollTop method from inside the for loop to outside of the loop.  
 Added translate and transform functions to reduce the number of layout recalculations.

```javascript
function updatePositions() {
  frame++;
  window.performance.mark("mark_start_frame");

  var items = document.querySelectorAll('.mover');
  var top = (document.body.scrollTop / 1250);

  for (var i = items.length; i--;) {
    var phase = Math.sin( top + (i % 5));
    var left = -items[i].basicLeft + 1000 * phase + 'px';
        items[i].style.transform = "translateX("+left+") translateZ(0)";
  }
```
