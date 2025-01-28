## Código de ejemplo con Three.js

Este es un ejemplo básico de cómo crear una línea en Three.js, renderizarla y mostrarla en el navegador.

```javascript
import * as THREE from 'three';

// Crear el renderizador WebGL
const renderer = new THREE.WebGLRenderer();
renderer.setSize( window.innerWidth, window.innerHeight );
document.body.appendChild( renderer.domElement );

// Crear la cámara con un campo de visión de 45 grados, relación de aspecto, y distancias de recorte
const camera = new THREE.PerspectiveCamera( 45, window.innerWidth / window.innerHeight, 1, 500 );
camera.position.set( 0, 0, 100 ); // Colocar la cámara a 100 unidades en el eje Z
camera.lookAt( 0, 0, 0 ); // Hacer que la cámara mire al origen

// Crear la escena
const scene = new THREE.Scene();

// Crear el material de la línea (color azul)
const material = new THREE.LineBasicMaterial( { color: 0x0000ff } );

// Definir los puntos de la línea
const points = [];
points.push( new THREE.Vector3( - 10, 0, 0 ) );
points.push( new THREE.Vector3( 0, 10, 0 ) );
points.push( new THREE.Vector3( 10, 0, 0 ) );

// Crear la geometría de la línea con los puntos
const geometry = new THREE.BufferGeometry().setFromPoints( points );

// Crear la línea con la geometría y el material
const line = new THREE.Line( geometry, material );

// Añadir la línea a la escena
scene.add( line );

// Renderizar la escena
renderer.render( scene, camera );