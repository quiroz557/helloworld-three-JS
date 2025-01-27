# React + Vite + Three JS

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react/README.md) uses [Babel](https://babeljs.io/) for Fast Refresh
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react-swc) uses [SWC](https://swc.rs/) for Fast Refresh


Instalar three.js 

    npm install --save three

Según lo entendido: 

 - Se crea una scena para renderizar el objeto.
    ```
        const scene = new THREE.Scene();
    ```
 - Se crea una camara para darle la visualización que queremos del objeto. (Perspectiva)
    ```
        const camera = new THREE.PerspectiveCamera( 50, window.innerWidth / window.innerHeight, 0.1, 1000 );
    ```
    - Parametros:
        1. 75: Este número es el campo de visión (FOV, por sus siglas en inglés, "Field of View") de la cámara, en grados. Un FOV de 75 significa que el ángulo de visión de la cámara es de 75 grados, lo que determina cuán amplio es el área visible de la escena. A mayor FOV, más ancha será la vista; a menor FOV, más estrecha.
        2. window.innerWidth / window.innerHeight: Este valor establece la relación de aspecto de la cámara (aspect ratio). Es la proporción entre el ancho y el alto de la ventana del navegador donde se muestra la escena. Esto es importante para asegurar que la imagen no se deforme cuando la ventana del navegador cambie de tamaño. El valor window.innerWidth devuelve el ancho de la ventana del navegador, y window.innerHeight devuelve la altura.
        3. 0.1: Este valor define el near clipping plane (plano de corte cercano). Es la distancia desde la cámara hasta el punto más cercano de la escena que se puede ver. Todo lo que esté más cerca que esta distancia no se renderizará.
        4. 1000: Este es el far clipping plane (plano de corte lejano). Es la distancia máxima desde la cámara hasta el punto más lejano que se puede ver. Cualquier objeto que esté más allá de esta distancia no se mostrará en la escena.

    En resumen, esta línea crea una cámara que tiene un campo de visión de 75 grados, ajustada al tamaño de la ventana del navegador, y con un rango de visibilidad de objetos entre 0.1 y 1000 unidades de distancia desde la cámara.

 - Creamos un geometry (una box o cualquier geometry que encuentras en la documentación como un div) esta box recibe 3 parametros: width:number, height: number, profundidad. Igual que las longitudes de un cubo.

    ```
    const geometry = new THREE.BoxGeometry( 1, 1, 1 );
    ```
 - Creamos un material. Esto es un objeto con los estilos a renderizar 
    ```
    const material = new THREE.MeshBasicMaterial( { color: 0x00ff00 } );
    ```
- Creamos un cubo. Para formar el cubo hacemos un mesh entre geometry y el material. 
    ```
    const cube = new THREE.Mesh( geometry, material );
    ```
- El cubo que creamos ya mezclado con el material y la geometría se lo añadimos a la scene
     ```
    scene.add( cube );
    ```
- posición z a la camara:

    Se utiliza para establecer la posición de la cámara en el espacio 3D en relación al eje Z.

    En Three.js (y en gráficos 3D en general), la cámara tiene tres coordenadas que definen su posición en el espacio tridimensional: x, y y z. Estos corresponden a los ejes en un sistema de coordenadas 3D:

        Eje X: Movimiento de izquierda a derecha.
        Eje Y: Movimiento de arriba a abajo.
        Eje Z: Movimiento hacia adelante y hacia atrás.

    La línea de código que mencionas está específicamente moviendo la cámara a lo largo del eje Z. El valor que asignas, en este caso 5, indica que la cámara estará a 5 unidades de distancia en el eje Z.
    ¿Qué significa esto?

    En un sistema de coordenadas 3D, si la cámara tiene una posición en z = 5, significa que la cámara está colocada a 5 unidades de distancia del origen de la escena (que normalmente está en z = 0).

        Si camera.position.z es 5, la cámara está alejada de la escena (viendo desde una distancia).
        Si pusieras camera.position.z = -5, la cámara estaría más cerca de la escena, o incluso podría estar mirando en la dirección opuesta, dependiendo de otros factores de la configuración de la cámara.

    ¿Por qué es importante?

    En 3D, la cámara tiene que estar ubicada en un punto determinado para poder ver la escena. Si no defines su posición correctamente, podría estar demasiado cerca o demasiado lejos de los objetos, o incluso dentro de ellos, lo que haría que no se vea nada correctamente.

    La posición de la cámara influye en cómo se renderiza la escena, ya que el sistema de coordenadas en Three.js sigue la regla de que un valor negativo en Z podría estar frente a la cámara (hacia donde está mirando), y un valor positivo indica que la cámara está mirando hacia la escena desde más lejos.
- Animamos el objeto:
    ```
    function animate() {

        cube.rotation.x += 0.01;
        cube.rotation.y += 0.01;

        renderer.render( scene, camera );
    }
    ```
- Renderizamos todo.
    ``` 
    import * as THREE from 'three';

    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera( 50, window.innerWidth / window.innerHeight, 0.1, 1000 );

    const renderer = new THREE.WebGLRenderer();
    renderer.setSize( window.innerWidth, window.innerHeight );
    document.body.appendChild( renderer.domElement );

    const geometry = new THREE.BoxGeometry( 1, 1, 1 );
    const material = new THREE.MeshBasicMaterial( { color: 0x00ff00 } );
    const cube = new THREE.Mesh( geometry, material );
    scene.add( cube );

    camera.position.z = 5;

    animate();

    function animate() {

        cube.rotation.x += 0.01;
        cube.rotation.y += 0.01;

        renderer.render( scene, camera );

    }
    ```


