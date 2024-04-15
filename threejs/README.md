# Three.js Sparknotes

Three.js is a powerful library for creating 3D graphics on the web, and grasping a few key topics can really help you get a significant understanding of its capabilities. According to the Pareto Principle, focusing on these core areas should provide the most substantial insight and functionality when using Three.js:

## Table of Contents
1. [Core Fundamentals](#core-fundamentals):

* **Scene**: Understanding what a scene is and how to add objects to it. This is the basic container for all your 3D objects.
* **Camera**: Learn about different types of cameras in Three.js, particularly the PerspectiveCamera, as it's most commonly used for 3D graphics. Knowing how to manipulate the camera’s position and viewing direction is crucial.
* **Renderer**: Get familiar with the WebGLRenderer, which handles the rendering of the scene as seen from the camera on a canvas.

2. [Geometry and Meshes](#geometries-and-meshes):
* **Basic Geometries**: Start with basic shapes like boxes, spheres, and planes. Knowing how to manipulate these can help you create more complex forms.
* **Mesh**: Understand what meshes are and how they are used to create 3D objects by combining geometry and materials.

3. [Lighting](#lighting):
* **Types of Light**: Learn about various types of lights such as AmbientLight, PointLight, DirectionalLight, and SpotLight. Lighting is critical for enhancing the mood, depth, and realism of a scene.
* **Shadows**: Understanding how to cast and receive shadows can significantly impact the visual fidelity of your scene.

4. [Materials and Textures](#material-and-textures):

* **Standard Materials**: Learn about the basic materials like `MeshBasicMaterial`, `MeshLambertMaterial`, and `MeshPhongMaterial`, and when to use each.
* **Textures**: Know how to apply textures to materials. Textures can dramatically change the appearance of objects and add details without increasing the geometric complexity.

5. [Animation and Interaction](#animation-and-interaction):

* **Animation Loops**: Learn how to use the animation loop to create movements and continuously render changes in your scene.
* **Interactivity**: Understand how to handle user inputs, such as mouse movements or clicks, to interact with objects in the scene.

By focusing on these key areas, you should be able to handle a wide range of tasks in Three.js and develop a solid understanding of how to create and manipulate 3D scenes in web environments. There are many more advanced topics and nuances within these categories, but mastering these fundamentals will give you a strong foundation in Three.js.

## Core Fundamentals

### 1. Scene
The scene in Three.js acts like a stage in theatre. It's an abstract space where all your 3D objects are placed and arranged. Everything you want to render or display using Three.js must be added to the scene. The scene object itself is a container for all types of objects such as lights, cameras, and mesh objects (which are combinations of a geometry and a material). To create and start using a scene, you typically initialize it with:

``` javascript
    const scene = new THREE.Scene();
```
This object is then populated with various 3D objects, lights, and other components.


### 2. Camera
Cameras in Three.js define the perspective from which the scene is viewed. One of the most commonly used cameras is the `PerspectiveCamera`, which simulates the way the human eye sees. It's characterized by a field of view, aspect ratio, near clipping plane, and far clipping plane. Here's how you might set up a perspective camera:

```javascript
const camera = new THREE.PerspectiveCamera(
  75, // field of view (degrees)
  window.innerWidth / window.innerHeight, // aspect ratio
  0.1, // near clipping plane
  1000 // far clipping plane
);
camera.position.set(0, 0, 5); // position the camera in space (x, y, z)
```
Understanding how to manipulate the camera's position and where it is looking is critical for navigating a 3D space visually.

### 3. Renderer
The renderer in Three.js takes the scene and a camera as inputs and renders that scene from the perspective of the camera onto a canvas. The most commonly used renderer is WebGLRenderer, which leverages WebGL to draw the scene. Here's a basic setup:

```javascript
const renderer = new THREE.WebGLRenderer({ antialias: true });
renderer.setSize(window.innerWidth, window.innerHeight); // set the size of the rendering window
document.body.appendChild(renderer.domElement); // add the renderer to the HTML document
```
The renderer's `render` method is called inside an animation loop or in response to user interaction or scene changes, to update what the user sees:

```javascript
function animate() {
  requestAnimationFrame(animate); // create a loop that causes the renderer to draw the scene every time the screen is refreshed (about 60 fps)
  renderer.render(scene, camera);
}
animate();
```

Each of these components plays a crucial role. The scene is your world, the camera is your eye, and the renderer is the tool that brings everything to the viewer. By mastering these three aspects, you can begin to explore the rich possibilities of creating 3D web experiences with Three.js.

## Geometry and Meshes

In Three.js, geometries and meshes are fundamental concepts used to create and manipulate 3D shapes. Understanding these concepts is crucial for effectively building and visualizing 3D models. Let's dive deeper into each of these aspects:

### 1. Geometries
Geometry in Three.js represents the shape or structure of a 3D object. It defines the vertices and faces (triangles) that make up the shape. Three.js comes with several predefined geometries that you can use to quickly create standard shapes. Here are a few common ones:

* **BoxGeometry**: Used to create a cube or rectangular prism.
* **SphereGeometry**: Used to create a spherical object.
* **PlaneGeometry**: Used to create a flat surface.
* **CylinderGeometry**: Used to create a cylindrical object.
* **TorusGeometry**: Used to create a donut-shaped object.


Here's an example of how to create a simple box geometry:

```javascript
const geometry = new THREE.BoxGeometry(1, 1, 1); // parameters: width, height, depth
```

Each geometry type takes specific parameters that define its size and shape. Customizing these parameters allows you to tailor the object's appearance to your needs.

### 2. Meshes
A mesh in Three.js is an object that combines geometry with material. Materials describe the appearance of the surface of the mesh, such as its color, texture, or reflectiveness. Here are some common materials:

MeshBasicMaterial: A material that is not affected by lights in the scene.
MeshLambertMaterial: A material that reflects light in a way that appears non-shiny (diffuse reflection).
MeshPhongMaterial: A material that simulates shiny surfaces with specular highlights.
Here’s how you create a mesh by combining geometry and material:

```javascript
const material = new THREE.MeshPhongMaterial({ color: 0x00ff00 }); // bright green
const cube = new THREE.Mesh(geometry, material);
scene.add(cube);
```

In this example, a cube mesh is created using the previously defined BoxGeometry and a green MeshPhongMaterial. This mesh is then added to the scene.

### 3. Manipulating Geometries and Meshes
Once you have a mesh, you can manipulate its position, rotation, and scale, which are crucial for arranging objects within the scene:

```javascript
cube.position.set(0, 0, 0);
cube.rotation.set(Math.PI / 4, 0, Math.PI / 4); // rotating the cube
cube.scale.set(2, 2, 2); // scaling the cube to double its size
```

These transformations are essential for creating dynamic and interactive 3D scenes. By understanding how to create and manipulate geometries and meshes, you can build complex and visually appealing 3D environments in your applications. This knowledge forms a foundational part of mastering Three.js, enabling you to develop more sophisticated 3D visualizations as you explore further into the library's capabilities.

## Lighting

Lighting is an essential aspect of Three.js and 3D graphics in general, as it adds realism and depth to scenes by defining how objects are illuminated. Let's delve deeper into the types of lights available in Three.js and their applications, as well as the concept of shadows which can greatly enhance the visual quality of your scene.

### Types of Lights
Three.js offers several types of lights that simulate real-world lighting conditions. Each type affects the scene and the materials in different ways:

1. Ambient Light:

    * This light globally illuminates all objects in the scene equally and without direction.
    * It’s useful for ensuring that no parts of the scene are completely dark.
    * Example:
        ```javascript
        const ambientLight = new THREE.AmbientLight(0xffffff, 0.5); // color and intensity
        scene.add(ambientLight);
        ```

2. Point Light:
   * A light that emits from a single point in all directions, similar to a light bulb.
   * Useful for creating realistic lighting effects and highlights on objects.
   * Example:
       ```javascript
       const pointLight = new THREE.PointLight(0xffffff, 1, 100); // color, intensity, and distance
       pointLight.position.set(10, 10, 10);
       scene.add(pointLight);
       ```
3. Directional Light:
   * Emulates sunlight, casting parallel light rays across the scene.
   * Great for simulating a light source that is very far away, like the sun.
   * Example:
        ```javascript
        const directionalLight = new THREE.DirectionalLight(0xffffff, 0.8);
        directionalLight.position.set(0, 1, 0);
        scene.add(directionalLight);
        ```
4. Spot Light:
    * A light that casts light in a cone shape.
    * Perfect for creating focused lighting effects or simulating flashlights or stage lights.
    * Example:
        ```javascript
        const spotLight = new THREE.SpotLight(0xffffff, 1);
        spotLight.position.set(15, 40, 35);
        spotLight.angle = Math.PI / 4;
        spotLight.penumbra = 0.1; // how much the light fades at the edges of the cone
        scene.add(spotLight);
        ```
### Understanding and Utilizing Shadows
Shadows add an extra layer of depth and realism to the scene. In Three.js, shadows are not automatically calculated due to performance reasons and need to be explicitly enabled both in the renderer and for each light and mesh that should cast or receive shadows.

* Enabling Shadows in the Renderer:
    * You must enable shadow mapping in the renderer:
        ```javascript
        renderer.shadowMap.enabled = true;
        renderer.shadowMap.type = THREE.PCFSoftShadowMap; // softer edges
        ```
* Configuring Lights to Cast Shadows:
    * Not all lights can cast shadows. Directional, point, and spot lights can cast shadows, but ambient lights cannot.
    * Example for a directional light:
        ```javascript
        directionalLight.castShadow = true;
        directionalLight.shadow.mapSize.width = 1024; // shadow resolution
        directionalLight.shadow.mapSize.height = 1024;
        ```
* Configuring Objects to Cast and Receive Shadows:
  * You also need to specify which objects in the scene can cast and receive shadows:
    ```javascript
    Copy code
    mesh.castShadow = true; // the object casts shadows
    mesh.receiveShadow = true; // the object receives shadows
    ```

Understanding these lighting and shadow techniques will significantly impact the visual quality of your 3D scenes. By carefully placing lights and configuring shadows, you can create dramatic, lifelike, and visually rich environments in Three.js.

## Material and Textures

In Three.js, materials and textures are vital components that define the surface appearance of 3D objects. Understanding these elements is key to creating visually engaging and realistic scenes. Let's explore more about materials and textures in Three.js:

### Materials:
Materials in Three.js determine how the geometry of a 3D object interacts with light and what it looks like visually. Here are some of the most commonly used materials and their characteristics:
1. MeshBasicMaterial:
   
    * This material does not react to any lighting, meaning it will not show shadows or highlights. It's useful for objects that you want to be uniformly lit regardless of lighting in the scene.
    * Example:
        ```javascript
        const material = new THREE.MeshBasicMaterial({ color: 0xff0000 }); // red color
        ```
2. MeshLambertMaterial:

   * This is a good general-purpose material with diffuse (non-shiny) reflection, ideal for matte surfaces.
   * It reacts to light in the scene, which can give a more realistic appearance under varied lighting conditions.
   * Example:
       ```javascript
       const material = new THREE.MeshLambertMaterial({ color: 0x00ff00 }); // green color
        ```
3. MeshPhongMaterial:

    * Suitable for shiny surfaces with specular highlights.
    * It simulates the light reflection you might see on glossy objects.
    * Example:
        ```javascript
        const material = new THREE.MeshPhongMaterial({ color: 0x0000ff, shininess: 100 }); // blue color, high shininess
        ```
4. MeshStandardMaterial (Physically-Based Rendering Material):

    * This is a physically accurate material suitable for all types of surfaces, from matte to shiny. It provides more realistic rendering by accurately simulating the interaction of light with surfaces.
    * Example:
        ```javascript
        const material = new THREE.MeshStandardMaterial({ color: 0xffffff, metalness: 0.5, roughness: 0.5 });
        ```
### Textures

Textures in Three.js are powerful tools used to add visual complexity to objects without adding additional polygons, making scenes more efficient and detailed. Here’s a more detailed exploration of how textures work in Three.js and how to effectively use them.

#### Texture Basics
A texture is essentially an image applied to the surface of a 3D object. This is done by mapping the 2D image over the object’s geometry in a process known as UV mapping, where each vertex in the geometry is assigned a coordinate in the image.

### Loading Textures
To use textures, you first need to load them with the TextureLoader class, which is asynchronous and ensures that the texture is fully loaded before it's used in the scene:

```javascript
const textureLoader = new THREE.TextureLoader();
const texture = textureLoader.load('path/to/your/image.jpg', function(texture) {
    // update materials or refresh the scene after the texture is loaded
    scene.add(mesh); // example of using the texture once it's ready
});
```

### Applying Textures to Materials
Once the texture is loaded, you can apply it to any material that accepts a map property, such as MeshBasicMaterial, MeshLambertMaterial, or MeshPhongMaterial. Here’s an example using MeshBasicMaterial:

```javascript
Copy code
const material = new THREE.MeshBasicMaterial({ map: texture });
const mesh = new THREE.Mesh(geometry, material);
```

### Common Uses of Textures
Textures can be used for various effects in a 3D scene:

* **Diffuse Maps**: These are the most common type of texture that define the object's surface color and details.
* **Bump Maps**: These simulate small-scale bumpiness on surfaces, affecting the material's normal at each point but not altering the geometry itself.
* **Normal Maps**: More complex than bump maps, normal maps alter the normals across the surface to simulate complex details like wrinkles or bumps, which affect how light reflects off the surface and do not change the object's actual shape.
* **Specular Maps**: These define the shininess and highlight colors on materials, telling the renderer which parts of the object are glossy.
* **Displacement Maps**: Unlike bump and normal maps, displacement maps actually modify the geometry, moving vertices based on the texture to create real geometric detail. This is more performance-intensive.

#### Advanced Texture Mapping Techniques
* **UV Mapping**: Properly mapping the texture coordinates is crucial. You can adjust UV coordinates in the geometry to control how the image wraps around the 3D shape.
* **Texture Wrapping and Repeat**: You can control how textures repeat (or tile) and how they behave at the edges. This is useful for creating seamless surfaces using a smaller texture image repeated multiple times.

    ```javascript
    Copy code
    texture.wrapS = THREE.RepeatWrapping;
    texture.wrapT = THREE.RepeatWrapping;
    texture.repeat.set(4, 4); // repeating the texture 4 times on each axis
    ```
* **Mipmaps and Filtering**: These are techniques used to improve texture appearance when viewed at a distance or at steep angles. Three.js automatically generates mipmaps for textures loaded via TextureLoader, which helps in scaling down textures smoothly.


By mastering these texturing techniques, you can significantly enhance the visual quality and performance of your 3D scenes in Three.js. Textures not only bring realism but also add a layer of depth and detail that can make simple geometries look incredibly complex and engaging.

## Animation and Interaction

In Three.js, animation and interaction are key aspects that can significantly enhance the engagement and realism of your 3D scenes. Let's delve deeper into how you can use these features to create dynamic and interactive experiences.

### Animation
Three.js provides a straightforward way to animate objects within the scene, which can include transformations such as translations, rotations, scaling, and changes in object properties like color or transparency. Animation is typically handled within the rendering loop, which updates the scene in real-time.

#### Creating an Animation Loop:
The animation loop is where you update the positions, rotations, or other properties of objects before re-rendering the scene. This loop runs continuously at a high frame rate to create smooth animations.

Here’s how you can set up a basic animation loop in Three.js:

```javascript
function animate() {
    requestAnimationFrame(animate); // Tell the browser you want to perform an animation

    // Update object properties
    mesh.rotation.x += 0.01;
    mesh.rotation.y += 0.01;

    // Render the scene again with the updated object properties
    renderer.render(scene, camera);
}
animate();
```
This loop continuously rotates a mesh around the x and y axes, creating a spinning effect.

### Interactivity
Interactivity involves responding to user inputs such as mouse clicks, mouse movements, keyboard presses, or touchscreen gestures to manipulate objects in the scene or change the camera's view.

#### Handling User Inputs:
You can add event listeners to the canvas or the document to capture and respond to user actions. Here’s a basic example of handling mouse movement to rotate a camera:

```javascript
function onDocumentMouseMove(event) {
    event.preventDefault();

    const mouseX = (event.clientX / window.innerWidth) * 2 - 1;
    const mouseY = -(event.clientY / window.innerHeight) * 2 + 1;

    camera.position.x += (mouseX - camera.position.x) * 0.05;
    camera.position.y += (mouseY - camera.position.y) * 0.05;
    camera.lookAt(scene.position);
}

document.addEventListener('mousemove', onDocumentMouseMove, false);
```
This script makes the camera subtly follow the mouse position, creating a more interactive viewing experience.

#### Click Events:
To make objects in the scene interactive (e.g., clicking on objects), you can use raycasting, which involves projecting a ray from the camera through the mouse position into the scene and detecting which objects it intersects.

```javascript
const raycaster = new THREE.Raycaster();
const mouse = new THREE.Vector2();

function onDocumentMouseClick(event) {
    event.preventDefault();

    mouse.x = (event.clientX / window.innerWidth) * 2 - 1;
    mouse.y = -(event.clientY / window.innerHeight) * 2 + 1;

    raycaster.setFromCamera(mouse, camera);
    const intersects = raycaster.intersectObjects(scene.children);

    if (intersects.length > 0) {
        console.log('Object clicked:', intersects[0].object);
    }
}

document.addEventListener('click', onDocumentMouseClick, false);
```

In this setup, clicking on an object in the scene logs that object to the console, which could be expanded to trigger other actions like opening an information panel or changing the object's color.

By combining animation and interactivity, you can create compelling 3D experiences that are both visually dynamic and engaging for users. These capabilities are crucial for applications in gaming, virtual reality, data visualization, and interactive web content.