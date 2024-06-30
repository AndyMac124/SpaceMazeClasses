# SpaceMaze Classes

### This repository holds the main Java classes I wrote in a minigame server without distributing other students code.

[View the demo video here](https://www.youtube.com/watch?v=0Q6NSY26P2c)

---
## Overview:
The SpaceMaze Game is a pacman-like game, where a player runs through a maze, hunting for the key (or keys) to unlock the exit.  The maze has bots, traps and a timer to challenge the player, as well as bonus chests and an end score to reward the player.

---
## Contents:
* [Overview](#overview)
* [User Story and Issues](#user-story)
* [How Does it work?](#how-does-it-work?)
* [Design Patterns](#design-pattern)
* [UML Class Diagram](#uml-class-diagram)
* [UML Sequence Diagram](#uml-sequence-diagram)
* [SpaceMaze Game Authors](#authors)

---
## User Story:
1. As a developer, I would like to create a pacman-style maze mini-game with a space theme.
2. As a player, I would like to play a challenging maze game with spaceships and aliens, that has rich features and user interface.

---
## Game Features:
* Space theme with attractive imagery
* Braid style maze
* Playable character
* Progression system via levels
* Time challenge
* Opponents and obstacles

---
## How does it work?
You, the Commander of the spaceship 'Millennium Seagull', are on a space mission to complete all levels in the asteroid maze as quickly as possible.  Race around the asteroid maze, avoiding the enemy alien bots and collect all the keys required to unlock the exit portal.  Your shields (lives) are only 5 alien encounters strong, so be careful!  There are wormholes and cosmic C4 that could be a help or hindrance to you, however the chests will buy you more time.  Good luck, Commander!

<details>
<summary> How <b>does</b> it work? </summary><br>

- A simple user interface provides the player with a vivid (but easy distinguish) braid-style maze and clear status bar to engage and assist the player during game play,
- The player can use either the arrow or W/A/S/D keys to move the player's avatar (the spaceship 'Millennium Seagull') through the maze,
- The alien bots seeks and chases the player,
- The player flies over the keys to collect them,
- The player can fly over the traps and bonuses to spring/use them,
- The portal exit will remain locked and red until the correct number of keys has been collected, then the portal will turn green and allow the player to exit (either to the next level or end of the game),
- The keys required are equal to the level number,
- The number of bots and keys required per level increases the difficulty for the player,
- The player has 5 lives, which can be depleted if they collide with an alien bot,
- The wormholes will take the player to a random location within the maze,
- The cosmic C4 (bombs) will blow up the walls around the player, but leave the player unharmed,
- The bonus chests returns 8 seconds to the player's timer,
- Achievements will be unlocked and stored in the Achievement API,


</details>

<details>

<summary> What does the game look like? </summary><br>

**Mockup Design:**

![SpaceMaze Game mockup](uploads/c815a4a1c15af6c3af592d2f97cfae1e/Design_mockup.PNG)

**Screenshots:**

![Start menu](uploads/e8b79fc1e9e09f0b9249b34be4ad8e87/Start_menu.PNG)

![Level 1](uploads/2e84e40dbdbbe3541e08436b03d989bd/lvl_1_ss.PNG)

**Video - Demo:**

![SpaceMaze Game Demo](https://www.youtube.com/watch?v=0Q6NSY26P2c)

</details>

<details>
<summary> What are the main parts of the code architecture? </summary><br>

The SpaceMaze game code is distributed over the javaprojects client, common and server directories.  We organized the following classes as such to keep much of the code server-side, however some elements such as basic player input validation, images and the SpaceBot class were stored client-side to assist with providing smoother and faster game play, by reducing server requests and better automating the bots movements.

### Client Classes:
- **SpaceMaze:** Class to set up the game window, communicate with the server and handle client-side processes.
- **MazeDisplay:** Class to display the maze array/graphics, handle player key inputs and do basic validation before sending player input server-side.
- **SpaceBot:** Class to store and control alien bots (within the maze) - derived from SpaceEntity.
- **Images:** Provides all client side classes access to the images used in the graphics.
- **SpaceMazeSound:** A class for basic sound effects in the game.
- **StatusBar:** A class for the UI status bar.

### Common Classes:
- **SpaceEntity:** An abstract class to use with the SpaceBot and SpacePlayer classes.

### Server Classes:
- **SpaceMazeServer:** Holds SpaceMaze games, interacts with client to receive player move commands and send updated mazeArray, and handles achievements.
- **SpaceMazeGame:** Represents an actual SpaceMaze game in progress.
- **MazeControl:** Contains logic to verify and update player's location in the maze, controls collisions with maze elements and allows access to an updated maze array to be displayed to the screen.
- **MazeInit:** Class to select the maze array for the current level.
- **GameTimer:** Class to track the elapsed time in a given game.
- **SpacePlayer:** Contains and handles the player's information (such as numLives, numKeys, playerScore) - derived from SpaceEntity.
- **InteractiveResponses:** Contains the game's interactive responses.

</details>

---
## Design Patterns:
One of the design patterns used within our game was:

**Singleton Pattern:**
- The Images class is an example of the Singleton Pattern, using static members to restrict the access of this class.  The Images class manages the images used to generate the graphics of the maze when called from MazeDisplay. This was done to to optimize the initialization and use of the images during game play.

The below did not follow the design pattern implementation rigidly, however in principle they are close:

**Singleton Pattern:**
- The MazeInit class demonstrates a pattern similar to the Singleton Pattern. This is because the server only uses one instance of the MazeInit class and has restricted access. The MazeInit class handles which maze array is being used for each level, and is only accessed via the getMazeInitArray() operation, which is only called from the MazeControl class upon the instantiation of each level. This singleton inspired idea was used to control concurrency issues with the mazeArray that might occur, so that there was only one point of access (the MazeControl class).


**Template Pattern:**
- The SpacePlayer and SpaceBot are both classes created using something similar to the Template Pattern. These classes are implemented via extending the same SpaceEntity abstract class. This method was used because there were some similarities on how the SpacePlayer and SpaceBot classes were to be designed and implemented, so having a point of origin that would handle the similarities made sense.

**Strategy Pattern:**
- The SpaceBots (the alien's class) demonstrates something similar to the strategy pattern. They patrol the maze by tracking the player and deciding where to move based on based on if it will bring it closer to the player. However, if the bot gets trapped (i.e. in a 'dead end' of the maze), the bot will change its patrol strategy to random (in an attempt to exit the 'dead end'), before returning to the tracking strategy.

---
## UML Class Diagram:

<details>
<summary>Client-side Class UML</summary>
![SpaceMaze Game UML Class Diagram - Client side](uploads/68ec992ed1c53dbe0c237928972659fa/Cient_side_4.png)
</details>

<details>
<summary>Server-side Class UML</summary>
![SpaceMaze Game UML Class Diagram - Server side](uploads/61d94ae0e88d33026c6149fec2547eb9/Server_side_3.png)
</details>

---
## UML Sequence Diagram:

<details>
<summary>Sequence Diagram</summary>
![SpaceMaze Game UML Sequence diagram](uploads/4751a307d5683ed1185203717dc2f9ce/Sequence_nested.png)

</details>


---
## Authors:
* Andrew McKenzie
* Natasha Hay
* Nikolas Olins
* Niraj Rana Bha



