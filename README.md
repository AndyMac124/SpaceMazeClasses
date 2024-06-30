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

</details>

---
## Design Patterns:
One of the design patterns used within our game was:

**Singleton Pattern:**
- The Images class is an example of the Singleton Pattern, using static members to restrict the access of this class.  The Images class manages the images used to generate the graphics of the maze when called from MazeDisplay. This was done to to optimize the initialization and use of the images during game play.



