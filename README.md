# Communicating Material Culture Diversity by Creating 3D Online or Virtual Reality Scenes or Games with Three.js (Part 2) (DRAFT)

## Kristine Hardy & Mathieu Leclerc

### This guide shows how to use the Three.js javascript library to create a simple puzzle website with 3D models to illustrate the diversity of the pottery technologies of communities in the Papua New Guinea area. The aim is to match the vessel to the community. Selecting a torus shows information about the pottery of that community and if the vessel is dragged onto the correct torus the background colour will change. The website is also able to be viewed in Virtual Reality (VR).

Puzzles can provide a way to engage an audience with 3D models....TODO

## Contents
- [Lesson Goals](#lesson-goals)
- [Software Requirements and Setting Up](#software-requirements-and-setting-up)
- [Designing the Game](#designing-the-game)
- [Adding Torus](#adding-torus)
- [Enabling Jar Movement](#enabling-jar-movement)
- [Enabling Jar Movement in VR](#enabling-jar-movement-in-vr)
- [Start Jars at Random Positions](#start-jars-at-random-positions)
- [Check for Successful Matches](#check-for-successful-matches)
- [Update the Instructions](#update-the-instructions)
- [Conclusion](#conclusion)


## Lesson Goals
text
## Software Requirements and Setting Up

See part 1. Recommended: a code editor, such as Visual Basic Code and a server such as Node.js.
This lesson presumes you are starting from the index.html file generated in part 1 and that the textures, models and main.css stylesheet are present. 

First check that everything is working with the index.html file from part 1, by opening the progect in Visual Studio Code, getting a New Terminal (Terminal > New Terminal), and typing 
```
npx serve
```
Go to your browser and enter the address given in the terminal (for example http://localhost:3000). To keep this simple we will start with the first 6 jars from part 1. If you added any of the other jars, comment out the code where you load the models. This can be done for single lines with //
```
//loader.load('models/gltf/kombio.glb', onLoadKombio, undefined, function ( error ) {console.error( error );} );
```
or put a /* at the beginning and a */ at the end of whole blocks that you want to comment out. You can also do this with the 'Toggle Block Comment' under Edit menu in VSC.
```
/* 
            all code here will be commented out...
 */
```

Check that 6 model jars are sitting on the map (you may have to move around to see them all). 

## Designing the Game

Plan and sketch the layout. How will the user know what to do? Is it only based on memory or logic? How is a successful match shown? Change the information panel used.

The goal for the user of this game is to start with the jars off the map and the PNG communities marked by selectable tokens. When the communities are selected (mouse click, or VR left controller) the information panel will provide the information on the pots made by that community. Information on how the technique used to make the pot can be used to work out which of the jars may be a match, as the jars are coloured by the technique and a key is provided. The decoration technique may also serve as a guide. The user can move the jars (mouse or VR right controller). If they place the matching jar on the community marker then the jar becomes unmoveable and the background colour changes. 


## Adding Torus

Green torus will be used to mark the communities. They can be harder to aim for than discs, but most PNG communities use torus made of leaves to hold the vessels as they are being made. The torus are a basic three.js geometry, and the diameter, central hole size, and segmentation can be specified. However, torus are generated at the wrong angle for this game and need to be rotated (around the x axis) by 90 degrees (ie -Math.PI *1/2).

Because each torus is connected to a different information plane, they still need to be created separately and added to a torus group. The mouse click event listener and left controller listeners have to be altered so that they target the torus group instead of the jar group.

In the index.html file REPLACE
```
let jars;
```

with 
```
let jars, torus;
```
in the init function after
```
	let piecescale = ratio;
```
add
```
	torus = new THREE.Group();
	scene.add( torus );

	const dimiriSite = new THREE.Mesh( new THREE.TorusGeometry(0.015, 0.007, 20, 20  ), new THREE.MeshStandardMaterial({color: 0x006400}));
	dimiriSite.position.set(0.43 *ratio, desk + 0.01, 0 *ratio);
	dimiriSite.scale.set( piecescale, piecescale, piecescale);
	dimiriSite.rotation.x = -Math.PI * 1/2;
	dimiriSite.userData.planes = dimiriG;
	torus.add(dimiriSite);

	const louisadeSite = new THREE.Mesh( new THREE.TorusGeometry( 0.015, 0.007, 20, 20 ), new THREE.MeshStandardMaterial({color: 0x006400}));
	louisadeSite.position.set(0.99* ratio, desk + 0.01, 0.59* ratio);
	louisadeSite.scale.set( piecescale, piecescale, piecescale);
	louisadeSite.rotation.x = -Math.PI * 1/2;
	louisadeSite.userData.planes = louisadeG;
	torus.add(louisadeSite);

	const mailuSite = new THREE.Mesh( new THREE.TorusGeometry( 0.015, 0.007, 20, 20 ), new THREE.MeshStandardMaterial({color: 0x006400}));
	mailuSite.position.set(0.84* ratio, desk + 0.01, 0.48* ratio);
	mailuSite.scale.set( piecescale, piecescale, piecescale);
	mailuSite.rotation.x = -Math.PI * 1/2;
	mailuSite.userData.planes = mailuG;
	torus.add(mailuSite);

	const adzeraSite = new THREE.Mesh( new THREE.TorusGeometry( 0.015, 0.007, 20, 20 ), new THREE.MeshStandardMaterial({color: 0x006400}));
	adzeraSite.position.set(0.61* ratio, desk + 0.01, 0.15* ratio);
	adzeraSite.scale.set( piecescale, piecescale, piecescale);
	adzeraSite.rotation.x = -Math.PI * 1/2;
	adzeraSite.userData.planes = adzeraG;
	torus.add(adzeraSite);

	const yabobSite = new THREE.Mesh( new THREE.TorusGeometry( 0.015, 0.007, 20, 20 ), new THREE.MeshStandardMaterial({color: 0x006400}));
	yabobSite.position.set(0.572* ratio, desk + 0.01, 0.0396* ratio);
	yabobSite.scale.set( piecescale, piecescale, piecescale);
	yabobSite.rotation.x = -Math.PI * 1/2;
	yabobSite.userData.planes = yabobG;
	torus.add(yabobSite);

	const aibomSite = new THREE.Mesh( new THREE.TorusGeometry( 0.015, 0.007, 20, 20 ), new THREE.MeshStandardMaterial({color: 0x006400}));
	aibomSite.position.set(0.36* ratio, desk + 0.01,-0.01* ratio);
	aibomSite.scale.set( piecescale, piecescale, piecescale);
	aibomSite.rotation.x = -Math.PI * 1/2;
	aibomSite.userData.planes = aibomG;
	torus.add(aibomSite);

	selectedTorus = aibomSite; 
```
save and check the torus appear on site reload.

in the onClick(event) function change
```
const intersects = raycasterM.intersectObjects( jars.children);	
```
to
```
const intersects = raycasterM.intersectObjects( torus.children);
```
save and check the mouse click and panel change now works on torus and not the jars.

in the getIntersections function change
```
return raycaster.intersectObjects( jars.children, false );
```
to 
```
return raycaster.intersectObjects( torus.children, false );
```
Save and check this works in VR if possible.

## Enabling Jar Movement

To be able to move the jars using the mouse, DragControls have to be imported and created.
After
```
    import { OrbitControls } from 'three/addons/controls/OrbitControls.js';
```
add
```
	import { DragControls } from 'three/addons/controls/DragControls.js';
```
change
```
	let camera, scene, renderer, controls;
```
to
```
	let camera, scene, renderer, controls, dragControls;
```
in the init function after
```
controls.update();

```
add
```
		dragControls = new DragControls( [ jars ], camera, renderer.domElement );
    	dragControls.addEventListener('dragstart', function (event) {
        	controls.enabled = false
    	})
    	dragControls.addEventListener('dragend', function (event) {
        	controls.enabled = true
		})	

```
save and reload and check that you can now move the jars around.
However, you will see that it can be difficult to move jars in certain positions in 3D. It is easier to achieve if you view the scene directly from the top or directly from the side. This is one of the benefits of using the game in VR, it is much easier to move the vessels in three dimensions.

## Enabling Jar Movement in VR

To simplify things the right controller will move jars and the left will select sites. Alterate listeners will be created and added to the right controller.

After
```
		const intersected = [];
```
add
```
		const intersected2 = [];
```

in the init function change
```
		controller2.addEventListener( 'selectstart', onSelectStart );
		controller2.addEventListener( 'selectend', onSelectEnd );
```
to
```
		controller2.addEventListener( 'selectstart', onSelectStart2 );
		controller2.addEventListener( 'selectend', onSelectEnd2 );
```
after
```
		function cleanIntersected() {
			while ( intersected.length ) {
				const object = intersected.pop();
				object.material.emissive.r = 0;
			}
		}
```
add
```
			function onSelectStart2( event ) {
				const controller = event.target;
				const intersections = getIntersections2( controller );
				if ( intersections.length > 0 ) {
					const intersection = intersections[ 0 ];
					const object = intersection.object;
					object.material.emissive.b = 0;
					controller.attach( object );
					controller.userData.selected = object;
				}
			}

			function onSelectEnd2( event ) {
				const controller = event.target;
				if ( controller.userData.selected !== undefined ) {
					const object = controller.userData.selected;
					object.material.emissive.b = 0;				
					jars.attach( object );							
					controller.userData.selected = undefined;
				}
			}

			function getIntersections2( controller ) {
				tempMatrix.identity().extractRotation( controller.matrixWorld );
				raycaster.ray.origin.setFromMatrixPosition( controller.matrixWorld );
				raycaster.ray.direction.set( 0, 0, - 1 ).applyMatrix4( tempMatrix );
				return raycaster.intersectObjects( jars.children, false );
			}

			function intersectObjects2( controller ) {
			// Do not highlight when already selected
			if ( controller.userData.selected !== undefined ) return;

				const line = controller.getObjectByName( 'line' );
				const intersections = getIntersections2( controller );

			if ( intersections.length > 0 ) {
				const intersection = intersections[ 0 ];
				const object = intersection.object;
				object.material.emissive.r = 1;
				intersected2.push( object );
				line.scale.z = intersection.distance;

			} else {
				line.scale.z = 5;
			}
		}
		function cleanIntersected2() {
			while ( intersected2.length ) {
				const object = intersected2.pop();
				object.material.emissive.r = 0;
			}
		}
```
Change the render function from;
```
    	function render() {
			cleanIntersected();
			intersectObjects( controller2 );
			intersectObjects( controller1 );
			renderer.render( scene, camera );
		}
```
to
```
		function render() {
				cleanIntersected();
				cleanIntersected2();
				intersectObjects( controller2 );
				intersectObjects2( controller1 );
				renderer.render( scene, camera );
			}
```
Save and check in VR.

## Start Jars at Random Positions

Change location to a random position within certain bounds, but store correct position in userData.

## Check for Successful Matches

At the end of each jar movement, check the distance between the jar and the correct position. Set allowed distance. Create a signal for the correct match.

## Update the Instructions

Lastly, to update the instructions in the first intro panel change the texture to the intro2.jpg
REPLACE
```
	const introTexture = textureLoader.load( 'textures/Intro.jpg' );
```
	
with
```
	const introTexture = textureLoader.load( 'textures/Intro2.jpg' );
```
save and check the new instructions appear.

## Conclusion

TODO. Possible to add a sound effect upon the correct jar match.

