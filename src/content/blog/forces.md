---
title: 'Forces'
description: 'Hed'
pubDate: 'Jun 19 2024'
heroImage: '/docs-placeholder-1.jpg'
order: 2
---
## Forces in Arquimedes.js

Forces are fundamental to simulating realistic physical behaviors in Arquimedes.js. They dictate how particles move by altering their velocity over time. This section explains how to create and apply forces, as well as how to use the `ForceBuilder` class to customize the forces in your simulation.

### Understanding Forces

In physics, a force is any interaction that, when unopposed, changes the motion of an object. In Arquimedes.js, forces are applied to particles and influence their acceleration based on their mass.

### Creating Forces

Forces in Arquimedes.js are created using the `ForceBuilder` class. This class provides various methods to define forces along different axes or with custom logic.

#### Basic Force Example

Here's how to create a simple force that constantly pushes a particle to the right (along the X-axis):

```javascript
import { ForceBuilder } from "arquimedes-js/physics/force";

// Apply a constant force to the right
const constantForceX = ForceBuilder.x(() => 10);

// Apply this force to a particle
particle.addForce(constantForceX);
```

#### Gravity Force Example

Gravity is a common force in physics simulations. To simulate gravity, you can create a downward force along the Y-axis:

```javascript
const gravity = ForceBuilder.y(p => -9.81 * p.mass.value);  // F = m * g

// Apply gravity to a particle
particle.addForce(gravity);
```

### Custom Forces

Custom forces can be created by providing a function that calculates the force based on the properties of the particle. This is useful for simulating more complex behaviors, such as springs or drag.

```javascript
// Custom force that decreases as the particle moves away from a point
const customForce = ForceBuilder.x(p => -0.5 * (p.position.x - 200));

// Apply the custom force to a particle
particle.addForce(customForce);
```

### ForceBuilder Methods

The `ForceBuilder` class provides several methods to create and customize forces:

- **`ForceBuilder.x(f)`**: Creates a force along the X-axis. The function `f` takes a particle as an argument and returns the magnitude of the force.

- **`ForceBuilder.y(f)`**: Creates a force along the Y-axis. The function `f` takes a particle as an argument and returns the magnitude of the force.

- **`ForceBuilder.from(f)`**: Creates a custom force vector. The function `f` takes a particle as an argument and returns a `Vector2D` representing the force.

Example of creating a force vector from a custom function:

```javascript
import { Vector2D } from "arquimedes-js/math/vectors";

// Create a custom force that pulls particles toward the origin (0, 0)
const attractionForce = ForceBuilder.from(p => {
    const direction = new Vector2D(-p.position.x, -p.position.y);
    return direction.normalize().scale(10);  // Scale the direction vector to represent the force magnitude
});

// Apply the attraction force to a particle
particle.addForce(attractionForce);
```

### Applying Multiple Forces

Particles can have multiple forces acting on them simultaneously. Each force will be applied during each update cycle, and their combined effect will determine the particle's acceleration and velocity.

```javascript
const windForce = ForceBuilder.x(() => 5);  // Simulate a wind force
const gravityForce = ForceBuilder.y(p => -9.81 * p.mass.value);  // Gravity

particle.addForce(windForce);
particle.addForce(gravityForce);
```

### Clearing Forces

If you need to remove all forces from a particle, you can use the `clearForces` method:

```javascript
particle.clearForces();  // Removes all applied forces from the particle
```

### Summary

Forces in Arquimedes.js are powerful tools for driving the motion of particles in your simulation. By using the `ForceBuilder` class, you can create simple or complex forces that interact with particles in various ways. Whether you're simulating gravity, applying custom forces, or combining multiple forces, understanding how to work with forces is key to building realistic physics simulations.