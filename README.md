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
- [Conclusion](#conclusion)


## Lesson Goals
text
## Software Requirements and Installation

See part 1. Recommended: a code editor, such as Visual Basic Code and a server such as Node.js.
This lesson presumes you are starting from the index.html file from part 1 and that the textures, models and main.css stylesheet are present. 

## Designing the Game

Plan and sketch the layout. How will the user know what to do? Is it only based on memory or logic? How is a successful match shown? Change the information panel used.

## Adding Torus

Add torus at positions of jars. Change so that torus selection triggers panel change. On click and in VR.

## Enabling Jar Movement

Adding drag controls.

## Enabling Jar Movement in VR

Adding attach to the controllers. Groups.

## Start Jars at Random Positions

Change location to a random position within certain bounds, but store correct position in userData.

## Check for Successful Matches

At the end of each jar movement, check the distance between the jar and the correct position. Set allowed distance. Create a signal for the correct match.

## Conclusion

TODO.

