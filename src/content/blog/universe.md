---
title: 'Universe'
description: 'Lorem'
pubDate: 'Jul 22 2022'
heroImage: '/docs-placeholder-2.jpg'
order: 4
---

## Universe and Renderer in Arquimedes.js

The **Universe** and **Renderer** are core components in Arquimedes.js that manage the simulation environment and how it is visualized. The `Universe` class handles the physics simulation, while different renderers like `P5UniverseRenderer` are used to visualize the particles and rigid bodies within the universe. This section covers how to set up and use these components to create dynamic simulations.

### The Universe

The `Universe` class acts as a container for all particles and rigid bodies in the simulation. It is responsible for updating the state of these entities over time, handling their interactions, and ensuring the correct application of forces and collision responses.

#### Creating a Universe

To start a simulation, you first need to create a `Universe` instance:

```javascript
import { Universe } from "arquimedes-js/universe";

// Create a new Universe instance
const universe = new Universe();
```

#### Adding Particles and Rigid Bodies

Particles and rigid bodies are added to the universe so that they can be part of the simulation. Once added, they will be updated and rendered automatically.

```javascript
// Add individual particles to the universe
universe.addParticle(particle1);
universe.addParticle(particle2);

// Add a rigid body to the universe
universe.addRigidBody(rigidbody);
```

#### Updating the Universe

The `next` method is called to advance the simulation by a time step `dt`. This method updates the positions, velocities, and interactions of all particles and rigid bodies within the universe.

```javascript
// Update the universe by a time step (dt)
universe.next(dt);
```

### Universe Renderer

The **Renderer** in Arquimedes.js is responsible for visualizing the simulation. Different renderers can be used depending on the desired output format or visualization style. The most common renderer is the `P5UniverseRenderer`, which uses the p5.js library to render the simulation.

#### P5UniverseRenderer

The `P5UniverseRenderer` is a built-in renderer that uses p5.js to draw particles and rigid bodies in a canvas. It handles the graphical representation of the universe's state.

##### Setting Up the Renderer

To use the `P5UniverseRenderer`, you first need to create an instance and pass it the universe that you want to visualize:

```javascript
import { P5UniverseRenderer } from "arquimedes-js/universe/renderers";

// Create a new P5UniverseRenderer instance and attach it to the universe
const renderer = new P5UniverseRenderer(universe);
```

##### Rendering the Universe

Rendering is typically done in a loop where the `render` method of the renderer is called repeatedly. This method updates the display based on the current state of the universe.

```javascript
import setFixedDeltaTimeout from "arquimedes-js/utils/fixedDeltaTime";

// Start the rendering loop with a fixed time step
setFixedDeltaTimeout((dt) => {
    renderer.render(dt);  // Render the universe for the given time step
}, 1 / 60);  // 60 FPS
```

##### Customizing the Render

The `P5UniverseRenderer` allows you to customize how particles and forces are visualized:

- **Particle Appearance**: The appearance of each particle is determined by its `Apparience` properties such as color, shape, width, and height.
- **Forces Visualization**: Forces acting on particles can be visualized as vectors, showing their direction and magnitude.

The renderer automatically draws the particles and forces based on these properties:

```javascript
renderer.render(dt);  // This method handles all drawing operations
```

### Summary

The `Universe` and `Renderer` classes in Arquimedes.js work together to manage and visualize physics simulations. The `Universe` handles the logic of the simulation, updating the state of particles and rigid bodies, while the `Renderer`—especially the `P5UniverseRenderer`—handles the visualization, bringing the simulation to life on screen. By understanding and utilizing these components, you can create dynamic and interactive physics simulations with realistic behavior and visual clarity.