---
title: 'Get started'
description: 'L'
pubDate: 'Jul 08 2022'
heroImage: '/docs-placeholder-3.jpg'
order: 0
---

## Getting Started with Arquimedes.js

Welcome to the **Arquimedes.js** documentation! This guide will help you get started with using Arquimedes.js, a 2D physics engine designed for creating realistic physics simulations. Whether you're a student learning about physics or an enthusiast looking to create animations, this guide will provide you with the basics to start your journey.

### Installation

To begin using Arquimedes.js, you need to install it via npm:

```bash
npm install arquimedes
```

### Basic Setup

Here’s a simple example to get you started with creating a universe and rendering it using p5.js:

```javascript
import { Universe } from "arquimedes-js/universe";
import { P5UniverseRenderer } from "arquimedes-js/universe/renderers";
import setFixedDeltaTimeout from "arquimedes-js/utils/fixedDeltaTime";

// Create a new Universe
const universe = new Universe();

// Initialize the renderer
const renderer = new P5UniverseRenderer(universe);

// Set up the render loop with a fixed delta time
setFixedDeltaTimeout((dt) => {
    renderer.render(dt);
}, 1 / 60); // Render at 60 FPS
```

### Creating Particles

Particles are the fundamental building blocks in Arquimedes.js. Below is an example of how to create and configure particles:

```javascript
import { Particle } from "arquimedes-js/physics";
import { Apparience } from "arquimedes-js/physics/particle";

// Create a new particle with specific properties
const particle = Particle.create()
    .setPosition(200, 200)
    .setMass(2)
    .setVelocity(50, 0)
    .setApparience(
        Apparience.create()
            .setWidth(50)
            .setHeight(50)
            .setColor("blue")
            .setShape("Circle")
            .build(),
    )
    .build();

// Add the particle to the universe
universe.addParticle(particle);
```

### Handling Collisions

To manage what happens when particles collide, you can use collision handlers:

```javascript
import { defaultCollisionHandler } from "arquimedes-js/collisions";

// Assign a default collision handler to a particle
particle.onCollision(defaultCollisionHandler);
```

### Adding Forces

You can apply forces to particles to simulate physics behavior such as gravity, thrust, or other forces:

```javascript
import { ForceBuilder } from "arquimedes-js/physics/force";

// Apply a horizontal force
particle.addForce(ForceBuilder.x(p => 0.01 * (300 - p.position.x)));
```

### Running the Simulation

Finally, use the `setFixedDeltaTimeout` function to continuously update and render your simulation:

```javascript
setFixedDeltaTimeout((dt) => {
    renderer.render(dt);
}, 1 / 60); // 60 FPS
```

### Next Steps

Now that you've got the basics, explore the rest of the documentation to learn more about advanced features, such as creating rigid bodies, custom forces, and more! Happy simulating!