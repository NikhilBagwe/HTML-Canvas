## Trail of circles using 'mousemove' :

```javascript
const canvas = document.getElementById('canvas1')
const ctx = canvas.getContext('2d')

canvas.width = window.innerWidth
canvas.height = window.innerHeight

window.addEventListener('resize', function () {
  canvas.width = window.innerWidth
  canvas.height = window.innerHeight
})

const mouse = {
  x: null,
  y: null,
}

const particlesArray = []

class Particle {
  constructor() {
    this.x = mouse.x
    this.y = mouse.y
    this.size = Math.random() * 15 + 1
    this.speedX = Math.random() * 3 - 1.5 // +ve - right, -ve = left along X axis
    this.speedY = Math.random() * 3 - 1.5
  }

  update() {
    this.x += this.speedX
    this.y += this.speedY
    // make the particles shrink
    if (this.size > 0.2) this.size -= 0.1
  }

  // draws a circle represnting a particle
  draw() {
    ctx.fillStyle = 'white'
    ctx.beginPath()
    ctx.arc(this.x, this.y, this.size, 0, Math.PI * 2)
    ctx.fill()
  }
}

// trigger 'draw' and 'update' methods of all particle objects
function handleParticles() {
  for (let i = 0; i < particlesArray.length; i++) {
    particlesArray[i].update()
    particlesArray[i].draw()

    // remove circle whose size is smaller than 0.3
    if (particlesArray[i].size <= 0.3) {
      particlesArray.splice(i, 1)
      i--
    }
  }
}

// push 10 new particle obj when we click
canvas.addEventListener('click', function (event) {
  mouse.x = event.x
  mouse.y = event.y
  for (let i = 0; i < 10; i++) {
    particlesArray.push(new Particle())
  }
})

// creates a trail of 4 circles on moving mouse
canvas.addEventListener('mousemove', function (event) {
  mouse.x = event.x
  mouse.y = event.y
  for (let i = 0; i < 5; i++) {
    particlesArray.push(new Particle())
  }
})

function animate() {
  ctx.clearRect(0, 0, canvas.width, canvas.height)
  handleParticles()
  requestAnimationFrame(animate)
}
animate()
```

## Fading the trail by drawing semi-transparent rectangle :

```javascript
function animate() {
  // Instead of using clearRect we will draw a semi-transparent rectangle over the canvas again and again.
  ctx.fillStyle = 'rgba(0,0,0,0.05)'
  ctx.fillRect(0, 0, canvas.width, canvas.height)
  handleParticles()
  requestAnimationFrame(animate)
}
animate()
```
