## Constellation effect :

- Same code as file 02
- Only in handleParticles() func we add a nested for loop
- Constellation effect is Acheived by comparing every particle within particlesArray with other particles in that array and if they are within a certain range from each other we draw a line between them
- We will use pythagorous theorem to calculate the distance between 2 particles i.e hypotenuse
```javascript
function handleParticles() {
  for (let i = 0; i < particlesArray.length; i++) {
    particlesArray[i].update()
    particlesArray[i].draw()

    for (let j = i; j < particlesArray.length; j++) {
      // Angle between this two sides is 90 deg. as we assume its right angle triangle
      const dx = particlesArray[i].x - particlesArray[j].x
      const dy = particlesArray[i].y - particlesArray[j].y
      // hypotenuse
      const distance = Math.sqrt(dx * dx + dy * dy)

      // if distance is less than 100 pixels draw a line
      if (distance < 100) {
        ctx.beginPath()
        ctx.strokeStyle = particlesArray[i].color
        ctx.lineWidth = 0.5
        // drawing line
        ctx.moveTo(particlesArray[i].x, particlesArray[i].y)
        ctx.lineTo(particlesArray[j].x, particlesArray[j].y)
        ctx.stroke()
        ctx.closePath()
      }
    }

    // remove circle whose size is smaller than 0.3
    if (particlesArray[i].size <= 0.3) {
      particlesArray.splice(i, 1)
      i--
    }
  }
}
```
