---
title: 'Rigidbodies'
description: 'Lore'
pubDate: 'Jul 15 2022'
heroImage: '/docs-placeholder-4.jpg'
order: 3
---
## Rigid Bodies and Particle Meshes in Arquimedes.js

In Arquimedes.js, rigid bodies represent collections of particles that move together while maintaining a fixed structure. Additionally, the concept of a **Particle Mesh** allows you to create structured arrangements of particles, such as grids or lattices, that can be treated as a single rigid body. This section covers how to create and manage rigid bodies and particle meshes, calculate their physical properties, and handle their motion and collisions.

### What is a Rigid Body?

A rigid body in Arquimedes.js is a system of particles that remain at fixed distances from one another. This allows the entire system to translate and rotate as a single unit, preserving its shape under the influence of forces.

### Creating a Rigid Body

You can create a rigid body by grouping multiple particles together. Here’s an example:

```javascript
import { Particle, Rigidbody } from "arquimedes-js/physics";

// Create individual particles
const particle1 = Particle.create().setPosition(100, 100).setMass(1).build();
const particle2 = Particle.create().setPosition(200, 100).setMass(1).build();
const particle3 = Particle.create().setPosition(150, 200).setMass(1).build();

// Create a rigid body from the particles
const rigidbody = Rigidbody.from([particle1, particle2, particle3]);

// Add the rigid body to the universe
universe.addRigidBody(rigidbody);
```

### Particle Meshes

A **Particle Mesh** is a grid or lattice structure of particles that can be used to create more complex rigid bodies. This is useful for simulations that require organized structures like grids, arrays, or even complex molecular structures.

#### Creating a Particle Mesh

You can use the `ParticleMeshBuilder` to easily create a grid of particles:

```javascript
import { Particle, ParticleMeshBuilder } from "arquimedes-js/physics/particle";
import { Vector2D } from "arquimedes-js/math/vectors";

// Define a basic particle template
const particleTemplate = Particle.create().setMass(1);

// Create a 5x5 grid of particles centered at (300, 300)
const particleMesh = Particle.mesh(particleTemplate)
    .setNumberOfParticles(5)   // Set the grid size
    .setSpacing(50)            // Set the spacing between particles
    .grid(new Vector2D(300, 300));

// Add each particle in the mesh to the universe
particleMesh.forEach(particle => universe.addParticle(particle));
```

In this example, `Particle.mesh()` creates a new `ParticleMeshBuilder` instance, which is then configured to create a grid of particles.

### Extending and Modifying Rigid Bodies

Once a rigid body or particle mesh is created, you can extend it by adding more particles:

```javascript
const particle4 = Particle.create().setPosition(250, 150).setMass(1).build();
rigidbody.add(particle4);

// Or extend with multiple particles
const particle5 = Particle.create().setPosition(300, 150).setMass(1).build();
const particle6 = Particle.create().setPosition(350, 150).setMass(1).build();
rigidbody.extend([particle5, particle6]);
```

### Physical Properties of Rigid Bodies and Particle Meshes

Rigid bodies and particle meshes share several key physical properties that define their behavior:

#### Center of Mass

The center of mass is the weighted average position of all particles in the rigid body or mesh, which acts as the pivot point for rotation.

```javascript
const centerOfMass = rigidbody.getCenterOfMass();
console.log(`Center of Mass: (${centerOfMass.x}, ${centerOfMass.y})`);
```

#### Moment of Inertia

The moment of inertia describes how resistant the body is to rotational motion around a specific axis. It’s calculated based on the distribution of mass within the body.

```javascript
const momentOfInertia = rigidbody.getMomentOfInertia();
console.log(`Moment of Inertia: ${momentOfInertia}`);
```

You can also calculate this property with respect to the center of mass:

```javascript
const momentOfInertiaCM = rigidbody.getMomentOfInertiaRespectMassCenter();
console.log(`Moment of Inertia (Center of Mass): ${momentOfInertiaCM}`);
```

### Motion and Dynamics of Rigid Bodies

Rigid bodies and particle meshes move as cohesive units. Arquimedes.js automatically handles the translation and rotation of these structures, ensuring that all particles maintain their relative positions.

#### Angular Velocity and Rotation

Angular velocity in rigid bodies is influenced by applied forces and the distribution of mass. Arquimedes.js calculates and applies this during each simulation update.

```javascript
rigidbody.next(deltaTime);  // Updates the rigid body's position and rotation
```

### Collision Handling

Rigid bodies and particle meshes can collide with other particles or rigid bodies in the simulation. Each particle within these structures can trigger collision events.

```javascript
import { defaultCollisionHandler } from "arquimedes-js/collisions";

// Assign a collision handler to each particle in the rigid body
rigidbody.getParticles().forEach(particle => {
    particle.onCollision(defaultCollisionHandler);
});
```

### Maintaining Structure: Distance Constraints

One of the essential features of rigid bodies and particle meshes is the maintenance of fixed distances between particles. This is automatically enforced during each simulation step to ensure the structure remains rigid.

```javascript
rigidbody.next(deltaTime);  // Enforces distance constraints
```

### Summary

Rigid bodies and particle meshes in Arquimedes.js provide powerful tools for simulating complex physical structures that need to maintain shape while interacting with forces and other objects in the environment. By leveraging the flexibility of particle meshes and the robustness of rigid bodies, you can create dynamic simulations of real-world objects and systems, ranging from simple grids to intricate mechanical systems.