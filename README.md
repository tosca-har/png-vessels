# Communicating Material Culture Diversity by Creating 3D Online or Virtual Reality Scenes or Games with Three.js (Part 2) (DRAFT)

## Kristine Hardy & Mathieu Leclerc

### This guide shows how to use the Three.js javascript library to create a simple puzzle website with 3D models to illustrate the diversity of the pottery technologies of communities in the Papua New Guinea area. The aim is to match the vessel to the community. Selecting a torus shows information about the pottery of that community and if the vessel is dragged onto the correct torus the background colour will change. The website is also able to be viewed in Virtual Reality (VR).

Puzzles can provide a way to engage an audience with 3D models....TODO

## Contents
- [Lesson Goals](#lesson-goals)
- [Software Requirements and Installation](#software-requirements-and-installation)
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
## Software Requirements and Installation

See part 1. Recommended: a code editor, such as Visual Basic Code and a server such as Node.js.
This lesson presumes you are starting from the index.html file generated in part 1 and that the textures, models and main.css stylesheet are present. 

## Designing the Game

Plan and sketch the layout. How will the user know what to do? Is it only based on memory or logic? How is a successful match shown? Change the information panel used.

The goal for the user of this game is to start with the jars off the map and the PNG communities marked by selectable tokens. When the communities are selected (mouse click, or VR left controller) the information panel will provide the information on the pots made by that community. Information on how the technique used to make the pot can be used to work out which of the jars may be a match, as the jars are coloured by the technique and a key is provided. The decoration technique may also serve as a guide. The user can move the jars (mouse or VR right controller). If they place the matching jar on the community marker then the jar becomes unmoveable and the background colour changes. 

## Adding Torus

Green torus will be used to mark the communities. They can be harder to aim for than discs, but most PNG communities use torus made of leaves to hold the vessels as they are being made. The torus are a basic three.js geometry, and the diameter, central hole size, and segmentation can be specified. However, torus are generated at the wrong angle for this game and need to be rotated (around the x axis) by 90 degrees (ie -Math.PI *1/2).

Because each torus is connected to a different information plane, they sill be created separately and added to a torus group. The mouse click event listener and left controller listeners have to be altered so that they target the torus group instead of the jar group.

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

Check that 6 model jars are sitting on the map (you may have to move around to see 1). 

In the index.html file REPLACE
let jars;

with 
```
let jars, torus;
```



## Enabling Jar Movement

Adding drag controls.

## Enabling Jar Movement in VR

Adding attach to the controllers. Groups.

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


## Conclusion

TODO.

