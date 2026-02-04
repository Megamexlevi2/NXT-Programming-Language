# NXT 3D Game Development Guide

## Introduction

NXT includes a complete 3D game engine that works 100% in the browser with no external dependencies! Everything you need to create 3D games is built right in.

## Quick Start

Here's a complete example to get you started:

```nxt
// Initialize the renderer
init canvas = document.getElementById("game")
init renderer = new game.Renderer(canvas)
renderer.setSize(800, 600)

// Create a scene and camera
init scene = new game.Scene3D()
init camera = new game.Camera(60, 800/600, 0.1, 1000)
camera.setPosition(0, 5, 10)
camera.lookAt(new game.Vector3(0, 0, 0))

// Create a cube
init cubeGeo = game.Primitives.cube(2)
init cubeMat = new game.Material({ color: game.Color.hex("#3498db") })
init cube = new game.Mesh(cubeGeo, cubeMat)
scene.add(cube)

// Add lighting
init light = new game.DirectionalLight(
  new game.Vector3(-1, -1, -1),
  game.Color.white,
  1
)
scene.add(light)

// Game loop
init gameLoop = new game.GameLoop(
  fn(dt) {
    // Update
    cube.rotation.y = cube.rotation.y + dt
  },
  fn() {
    // Render
    renderer.render(scene, camera)
  }
)

gameLoop.start()
```

---

## 3D Math

### Vector3 (3D Points and Directions)

```nxt
// Create vectors
init pos = new game.Vector3(10, 20, 30)
init vel = new game.Vector3(1, 0, 0)

// Operations
pos.add(vel)      // Add vectors
pos.sub(vel)      // Subtract vectors
pos.mul(2)        // Multiply by number
pos.div(2)        // Divide by number
pos.dot(vel)      // Dot product
pos.cross(vel)    // Cross product
pos.length()      // Get length
pos.normalize()   // Make length = 1
pos.distance(vel) // Distance between points
pos.lerp(vel, 0.5) // Interpolate

// Rotation
pos.rotateX(0.5)  // Rotate around X axis
pos.rotateY(0.5)  // Rotate around Y axis
pos.rotateZ(0.5)  // Rotate around Z axis

// Special vectors
game.Vector3.zero()    // (0, 0, 0)
game.Vector3.one()     // (1, 1, 1)
game.Vector3.up()      // (0, 1, 0)
game.Vector3.forward() // (0, 0, -1)
game.Vector3.right()   // (1, 0, 0)
```

### Matrix4 (Transformations)

```nxt
init matrix = new game.Matrix4()

// Transform operations
matrix.translate(x, y, z)
matrix.scale(x, y, z)
matrix.rotateX(angle)
matrix.rotateY(angle)
matrix.rotateZ(angle)

// Camera matrices
matrix.perspective(fov, aspect, near, far)
matrix.orthographic(left, right, bottom, top, near, far)
matrix.lookAt(eye, target, up)

// Utilities
matrix.invert()
matrix.multiply(otherMatrix)
matrix.transformVector(vector)
```

### Quaternion (Smooth Rotations)

```nxt
init rotation = new game.Quaternion()

// Create from different sources
game.Quaternion.fromAxisAngle(axis, angle)
game.Quaternion.fromEuler(x, y, z)

// Operations
rotation.multiply(other)
rotation.conjugate()
rotation.normalize()
rotation.slerp(other, t)  // Smooth interpolation
rotation.rotateVector(vector)
rotation.toMatrix()
```

---

## Geometry

### Built-in Shapes

```nxt
// Cube
init cube = game.Primitives.cube(size)

// Sphere
init sphere = game.Primitives.sphere(radius, segments, rings)

// Plane/Floor
init plane = game.Primitives.plane(width, height, segmentsW, segmentsH)

// Cylinder
init cylinder = game.Primitives.cylinder(radiusTop, radiusBottom, height, segments)

// Cone
init cone = game.Primitives.cone(radius, height, segments)

// Torus (Donut)
init torus = game.Primitives.torus(radius, tubeRadius, radialSegments, tubularSegments)
```

### Custom Geometry

```nxt
init geo = new game.Geometry()

// Add vertices
geo.vertices.push(new game.Vector3(0, 1, 0))
geo.vertices.push(new game.Vector3(-1, 0, 0))
geo.vertices.push(new game.Vector3(1, 0, 0))

// Add face indices
geo.indices.push(0, 1, 2)

// Calculate normals
geo.computeNormals()
```

---

## Materials

```nxt
// Basic material
init material = new game.Material({
  color: { r: 1, g: 0, b: 0 },  // Red
  ambient: 0.1,
  diffuse: 0.8,
  specular: 0.5,
  shininess: 32,
  opacity: 1,
  wireframe: false
})

// Using color helpers
init blue = new game.Material({ color: game.Color.hex("#3498db") })
init green = new game.Material({ color: game.Color.rgb(0, 255, 0) })
init random = new game.Material({ color: game.Color.random() })
```

---

## Meshes (3D Objects)

```nxt
init geometry = game.Primitives.cube(1)
init material = new game.Material({ color: game.Color.blue })
init mesh = new game.Mesh(geometry, material)

// Position
mesh.setPosition(x, y, z)
mesh.position = new game.Vector3(x, y, z)

// Rotation
mesh.setRotation(x, y, z)  // Euler angles
mesh.rotateX(angle)
mesh.rotateY(angle)
mesh.rotateZ(angle)

// Scale
mesh.setScale(x, y, z)
mesh.setScale(2)  // Uniform scale

// Visibility
mesh.visible = true
mesh.visible = false
```

---

## Cameras

### Perspective Camera (Normal 3D View)

```nxt
init camera = new game.Camera(
  60,      // FOV (field of view) in degrees
  16/9,    // Aspect ratio
  0.1,     // Near plane
  1000     // Far plane
)

camera.setPosition(0, 5, 10)
camera.lookAt(new game.Vector3(0, 0, 0))
```

### First Person Camera

```nxt
init camera = new game.FirstPersonCamera(60, 16/9, 0.1, 1000)
camera.setPosition(0, 2, 0)
camera.moveSpeed = 10
camera.lookSpeed = 0.002

// In game loop
fn update(dt) {
  // Look around
  camera.rotate(mouse.dx, mouse.dy)
  
  // Move
  if game.Input.isKeyDown("KeyW") {
    camera.moveForward(dt)
  }
  if game.Input.isKeyDown("KeyS") {
    camera.moveForward(-dt)
  }
  if game.Input.isKeyDown("KeyA") {
    camera.moveRight(-dt)
  }
  if game.Input.isKeyDown("KeyD") {
    camera.moveRight(dt)
  }
}
```

### Orbit Camera

```nxt
// Orbit around a point
var azimuth = 0
var elevation = 0.5
var distance = 10

fn update(dt) {
  azimuth = azimuth + 0.01
  camera.orbit(azimuth, elevation, distance)
}
```

---

## Lights

### Directional Light (Sun)

```nxt
init sun = new game.DirectionalLight(
  new game.Vector3(-1, -1, -1),  // Direction
  game.Color.white,              // Color
  1                               // Intensity
)
scene.add(sun)
```

### Point Light (Bulb)

```nxt
init lamp = new game.PointLight(
  new game.Vector3(0, 5, 0),  // Position
  game.Color.yellow,           // Color
  1,                           // Intensity
  10                           // Range
)
scene.add(lamp)
```

### Spot Light (Flashlight)

```nxt
init flashlight = new game.SpotLight(
  new game.Vector3(0, 5, 0),  // Position
  new game.Vector3(0, -1, 0), // Direction
  game.Color.white,            // Color
  1,                           // Intensity
  Math.PI / 4,                 // Angle
  10                           // Range
)
scene.add(flashlight)
```

### Ambient Light (Everywhere)

```nxt
scene.ambientLight = new game.AmbientLight(
  game.Color.white,
  0.2  // Low intensity for subtle effect
)
```

---

## Collision Detection

### Bounding Box

```nxt
init box = new game.BoundingBox(
  new game.Vector3(-1, -1, -1),  // Min
  new game.Vector3(1, 1, 1)      // Max
)

box.contains(point)      // Is point inside?
box.intersects(otherBox) // Do boxes overlap?
box.center()             // Get center point
box.size()               // Get dimensions
```

### Bounding Sphere

```nxt
init sphere = new game.BoundingSphere(
  new game.Vector3(0, 0, 0),  // Center
  5                            // Radius
)

sphere.contains(point)
sphere.intersects(otherSphere)
sphere.intersectsBox(box)
```

### Raycasting

```nxt
init ray = new game.Ray(
  camera.position,                           // Origin
  camera.target.sub(camera.position).normalize()  // Direction
)

// Check intersections
init hitBox = ray.intersectsBox(boundingBox)
init hitSphere = ray.intersectsSphere(boundingSphere)
init hitPlane = ray.intersectsPlane(normal, distance)
init hitTriangle = ray.intersectsTriangle(v0, v1, v2)

if hitBox {
  print("Hit at distance: " + hitBox)
  init hitPoint = ray.at(hitBox)
}
```

---

## Input

```nxt
// Initialize
game.Input.init(canvas)

// Keyboard
game.Input.isKeyDown("KeyW")      // W key
game.Input.isKeyDown("Space")     // Spacebar
game.Input.isKeyDown("ShiftLeft") // Left Shift

// Mouse
game.Input.isMouseDown(0)  // Left click
game.Input.isMouseDown(1)  // Middle click
game.Input.isMouseDown(2)  // Right click
game.Input.mouse.x         // Mouse X position
game.Input.mouse.y         // Mouse Y position
game.Input.mouse.dx        // Mouse movement X
game.Input.mouse.dy        // Mouse movement Y

// Reset mouse deltas after processing
game.Input.resetMouse()
```

---

## Game Loop

```nxt
init loop = new game.GameLoop(
  fn(deltaTime) {
    // UPDATE - Called every frame
    // deltaTime is seconds since last frame
    
    player.position = player.position.add(
      player.velocity.mul(deltaTime)
    )
  },
  fn() {
    // RENDER - Called after update
    renderer.render(scene, camera)
  }
)

// Start the loop
loop.start()

// Get FPS
print(loop.fps)

// Stop the loop
loop.stop()
```

---

## Complete Game Example

Here's a simple 3D game with a player that can move around:

```nxt
// Setup
init canvas = document.getElementById("game")
init renderer = new game.Renderer(canvas)
renderer.setSize(window.innerWidth, window.innerHeight)

init scene = new game.Scene3D()
init camera = new game.FirstPersonCamera(60, window.innerWidth / window.innerHeight, 0.1, 1000)
camera.setPosition(0, 2, 5)

// Create floor
init floorGeo = game.Primitives.plane(50, 50)
init floorMat = new game.Material({ color: game.Color.hex("#2ecc71") })
init floor = new game.Mesh(floorGeo, floorMat)
scene.add(floor)

// Create some cubes
for i in [0, 1, 2, 3, 4] {
  init cubeGeo = game.Primitives.cube(1)
  init cubeMat = new game.Material({ color: game.Color.random() })
  init cube = new game.Mesh(cubeGeo, cubeMat)
  cube.setPosition(
    game.Math.randomRange(-10, 10),
    0.5,
    game.Math.randomRange(-10, 10)
  )
  scene.add(cube)
}

// Add lighting
init sun = new game.DirectionalLight(
  new game.Vector3(-0.5, -1, -0.5),
  game.Color.white,
  1
)
scene.add(sun)
scene.ambientLight = new game.AmbientLight(game.Color.white, 0.3)

// Initialize input
game.Input.init(canvas)

// Game loop
init loop = new game.GameLoop(
  fn(dt) {
    // Mouse look
    camera.rotate(game.Input.mouse.dx, game.Input.mouse.dy)
    game.Input.resetMouse()
    
    // Movement
    if game.Input.isKeyDown("KeyW") { camera.moveForward(dt) }
    if game.Input.isKeyDown("KeyS") { camera.moveForward(-dt) }
    if game.Input.isKeyDown("KeyA") { camera.moveRight(-dt) }
    if game.Input.isKeyDown("KeyD") { camera.moveRight(dt) }
    if game.Input.isKeyDown("Space") { camera.moveUp(dt) }
    if game.Input.isKeyDown("ShiftLeft") { camera.moveUp(-dt) }
  },
  fn() {
    renderer.render(scene, camera)
  }
)

loop.start()
print("Game started! WASD to move, mouse to look.")
```

---

## Utility Functions

```nxt
// Angle conversion
game.degToRad(90)   // Degrees to radians
game.radToDeg(1.57) // Radians to degrees

// Math helpers
game.clamp(value, min, max)
game.lerp(a, b, t)  // Linear interpolation
game.smoothstep(a, b, t)

// Random numbers
game.random(0, 10)     // Float between 0-10
game.randomInt(0, 10)  // Integer between 0-10
```

---

## Tips for Better Games

1. **Use deltaTime** - Multiply movement by deltaTime to make it frame-rate independent
2. **Batch similar objects** - Objects with the same geometry/material render faster
3. **Use bounding boxes** - They're faster than checking individual triangles
4. **Limit lights** - Too many lights slow down rendering
5. **Lower poly counts** - Use fewer segments for spheres/cylinders on mobile

Happy 3D game making!
