# **Tinykinesis**

> ESMA - Rennes   
> Student Project - 2024-2025 - 8 months - **Actually in production**  
> Unreal Engine 5 - Blueprint/C++  
> Team of 10    
> System Programmer, Environment programmer, Level Designer


<img src="https://github.com/AshiyroMisachi/RiallotAlexandre_Portfolio/blob/main/Projects/Tinykinesis/Assets/LogoProvisoire.png" width="400" height="400">


## **Context**

During my studies at ESMA, the graduation project was the conception of a full Vectical Slice of a game. In the end of my second year, with two friends, we make and presented Tinykinesis and got selected!

The game is a hoard shooter where you use telekinesis as a weapon. As Spark, a little fairy, you have to defend an attraction park of an invasion by beating little monsters! 

The game will take place in 3 differents level where you will have to defeat wave of ennemies in different arena with the objective to save the park. 


## **What I Did**

Because my portfolio and I are oriented on programmation, I will not talk about my Level Design work who was in first part more important for the project.

### **System Programmer**

I coded how the arena where the player will fight ennemies works.   
For that, I started first with the Game Designe how the arena should work and what was the "rules". 

I used a lot of list to store information about ennemis presence or spawn and the use of Map to update the difficulty of the Arena based on ennemies kills.

After prototyping the ArenaManager, I decided to make a simple tool to help the use of ArenaManager, in fact, there is a lot of list who need to be setup who can be very painfull. I make a Editor Utility Widget to simplify this.   

![EUW ArenaManager](https://github.com/AshiyroMisachi/RiallotAlexandre_Portfolio/blob/main/Skills/Assets/Image/UE_ArenaManagerTools.PNG)


Later, when we will validating the system of Arena, I will refactoring the ArenaManager to be more compact.

### **Environment Programmer**

I was in charge to create all the various thing the player can interract in the environnement. 

I used the hierarchy to create a system of destructible object to quickly design and test new behaviours from blueprint.

I created actors with Event Dispatcher System to add events depending of the context with like LevelSequence to animate object.


## **What I learned**

It was my first big project on Unreal Engine, so I learned the workflow of Blueprint/C++ and deepen my knowledge about UE5.

It was also the first time I did a project with more than 5 people, I learned to listen and work the needs of everyone in a team. 

We did a pre-production and a production in this school's project. I could employ what I have learn in pre-production and production to prevent conflicts and problems. 

## **More about the Project**

* [Test the game!](https://barna-bus.itch.io/tinykinesis)

***
  


[Get back to the project page](https://github.com/AshiyroMisachi/RiallotAlexandre_Portfolio/blob/main/Projects/Projects.md)    
[Get back to the main page](https://github.com/AshiyroMisachi/RiallotAlexandre_Portfolio)