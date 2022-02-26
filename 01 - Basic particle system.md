## Template code for creating a particle system in canvas

```javascript
class Particle {
  constructor() {
    // this.x = mouse.x
    // this.y = mouse.y
    this.x = Math.random() * canvas.width
    this.y = Math.random() * canvas.height
    // size of particle
    this.size = Math.random() * 5 + 1
    // We want our particle to move in all directions, we assign +ve and -ve values randomly
    this.speedX = Math.random() * 3 - 1.5 // +ve - right, -ve = left along X axis
    this.speedY = Math.random() * 3 - 1.5
  }

  // changes the direction coordinates
  update() {
    this.x += this.speedX
    this.y += this.speedY
    // make the particles shrink
    if (this.size > 0.2) this.size -= 0.1
  }

  // draws a circle represnting a particle
  draw() {
    ctx.fillStyle = 'blue'
    ctx.beginPath()
    ctx.arc(this.x, this.y, 50, 0, Math.PI * 2)
    ctx.fill()
  }
}

const particlesArray = []

// create 100 particle obj and push them into particles array
function init() {
  for (let i = 0; i < 100; i++) {
    particlesArray.push(new Particle())
  }
}

init()

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

// Animation loop
function animate() {
  ctx.clearRect(0, 0, canvas.width, canvas.height)
  handleParticles()
  requestAnimationFrame(animate)
}
animate()
```
