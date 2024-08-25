---
title: 'Particles'
description: 'He'
pubDate: 'Jun 19 2024'
heroImage: '/docs-placeholder-1.jpg'
order: 1
---

## Particles in Arquimedes.js

Particles are the core entities in Arquimedes.js that represent physical objects in the simulation. They can interact with each other, experience forces, and respond to collisions. This section provides an in-depth overview of how to create, configure, and manipulate particles within your simulations.

### Creating a Particle

To create a particle, you use the `ParticleBuilder` class. This builder pattern allows you to set various properties of the particle before adding it to the universe.

```javascript
import { Particle } from "arquimedes-js/physics";

// Create a simple particle
const particle = Particle.create()
    .setPosition(100, 100)   // Set the initial position
    .setMass(1)              // Set the mass of the particle
    .setVelocity(10, 0)      // Set the initial velocity
    .build();                // Build the particle

// Add the particle to the universe
universe.addParticle(particle);
```

### Particle Properties

When creating a particle, you can define several properties to control its behavior in the simulation:

- **Position**: The initial position of the particle in the 2D space, set using `setPosition(x, y)`.
- **Velocity**: The initial velocity vector of the particle, set using `setVelocity(x, y)`. This determines the speed and direction of the particle’s movement.
- **Mass**: The mass of the particle, which affects how forces influence its movement, set using `setMass(value)`.
- **Charge**: The electric charge of the particle, if relevant to your simulation, set using `setCharge(value)`.

### Particle Appearance

The appearance of a particle can be customized using the `Apparience` class. This includes properties like shape, color, width, and height.

```javascript
import { Apparience } from "arquimedes-js/physics/particle";

// Create a particle with custom appearance
const particleWithAppearance = Particle.create()
    .setPosition(150, 150)
    .setMass(2)
    .setApparience(
        Apparience.create()
            .setWidth(30)
            .setHeight(30)
            .setColor("red")
            .setShape("Circle")   // Shape can be "Circle" or "Box"
            .build(),
    )
    .build();

universe.addParticle(particleWithAppearance);
```

### Forces and Behaviors

Particles in Arquimedes.js can have forces applied to them, which will alter their velocity over time. You can add multiple forces to a particle, and these will be applied during each update cycle of the simulation.

```javascript
import { ForceBuilder } from "arquimedes-js/physics/force";

// Apply a gravitational force to a particle
particle.addForce(ForceBuilder.y(p => -9.81 * p.mass.value));

// Clear all forces from a particle
particle.clearForces();
```

Additionally, particles can have custom behaviors, which are functions that are executed during each update cycle. These behaviors can be used to implement complex dynamics.

```javascript
// Add a custom behavior to oscillate the particle horizontally
particle.addBehaviour(p => {
    const frequency = 0.5;
    p.position.x += Math.sin(frequency * Date.now() / 1000);
});
```

### Collision Handling

Collision detection is a crucial part of any physics engine. In Arquimedes.js, you can define what happens when a particle collides with another particle by attaching collision callbacks.

```javascript
import { defaultCollisionHandler } from "arquimedes-js/collisions";

// Attach a default collision handler to the particle
particle.onCollision(defaultCollisionHandler);

// Or create a custom collision handler
particle.onCollision((self, other) => {
    // Custom collision response logic
    console.log(`Collision detected between ${self} and ${other}`);
});
```

### Advanced: Particle Meshes

For more complex simulations, you might want to create a group of particles arranged in a specific pattern, such as a grid. This is possible using the `ParticleMeshBuilder`.

```javascript
import { Particle } from "arquimedes-js/physics/particle";
import { ParticleMeshBuilder } from "arquimedes-js/physics/particle";

// Create a 3x3 grid of particles centered at (200, 200)
const grid = Particle.mesh(Particle.create().setMass(1))
    .setNumberOfParticles(3)
    .setSpacing(50)
    .grid(new Vector2D(200, 200));

// Add all particles in the grid to the universe
grid.forEach(particle => universe.addParticle(particle));
```

### Summary

Particles are versatile and essential components of Arquimedes.js, capable of simulating a wide range of physical behaviors. By understanding and utilizing their properties, appearance, forces, behaviors, and collision handling, you can create rich and dynamic simulations that mimic real-world physics.
