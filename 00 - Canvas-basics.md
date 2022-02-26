# Getting started :

- Create a canvas element in HTML file.
- Store it's reference into a variable in JS file.
- Then call 'getContext' on 'canvas' variable and returns a built-in canvas 2D drawing api object

```javascript
const canvas = document.getElementById('canvas1')

// we call 'getContext' on 'canvas' variable and returns a built-in canvas 2D drawing api object
const ctx = canvas.getContext('2d')
console.log(ctx)
```

## Prevent canvas from streching on resizing window and Drawing rectangle :

```javascript
canvas.width = window.innerWidth
canvas.height = window.innerHeight

// drawing a rectangle in canvas - this will be rendered only once when page is loaded, so we include it inside event listener below.
// ctx.fillStyle = 'white'
// ctx.fillRect(10, 20, 150, 50)

window.addEventListener('resize', function () {
  canvas.width = window.innerWidth
  canvas.height = window.innerHeight
  ctx.fillStyle = 'white'
  ctx.fillRect(10, 20, 150, 50)
})
```

## Drawing a circle on click :

- Below code draws a circle on screen wherever we click

```javascript
// obj to store coordinates of mouse click
const mouse = {
  x: null,
  y: null,
}

// Function to Draw a circle 
function drawCircle() {
  ctx.fillStyle = 'red'
  ctx.strokeStyle = 'white'
  // border thickness
  //ctx.lineWidth = 15
  // tells JS we are drawing a new shape
  ctx.beginPath()
  ctx.arc(mouse.x, mouse.y, 50, 0, Math.PI * 2)
  // fills the circle with red color
  ctx.fill()
  // draws a border only
  ctx.stroke()
}
//drawCircle()

// 'click' event listener to draw circle wherever we click on canvas
canvas.addEventListener('click', function (event) {
  // stores coordinates where we clicked into obj
  mouse.x = event.x
  mouse.y = event.y
  drawCircle()
})
```

## Simple Brush - draw circles while moving cursor :

```javascript
canvas.addEventListener('mousemove', function (event) {
  // stores coordinates where we clicked into 'x'
  mouse.x = event.x
  mouse.y = event.y
  drawCircle()
})
```

## Animation loop - Make a circle follow the cursor :

- The animate func is called continously so the circle is drawed also and prev circle drawn by 'mousemove' event listener is cleared simultaneously.

```javascript
canvas.addEventListener('mousemove', function (event) {
  // stores coordinates where we clicked into 'x'
  mouse.x = event.x
  mouse.y = event.y
  drawCircle()
})

// Animation loop 
function animate() {
  ctx.clearRect(0, 0, canvas.width, canvas.height)
  drawCircle()
  requestAnimationFrame(animate)
}

animate()
```







