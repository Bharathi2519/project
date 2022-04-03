# Introduction


- The game involves controlling a single block or snakehead by turning only left or right by ninety degrees until you manage to eat an apple. When you get the apple, the Snake grows an extra block or body segment.
- If, or rather when, the snake bumps into the edge of the screen or accidentally eats himself the game is over. The more apples the snake eats the higher the score

## Features

- Snake game is a computer action game, whose goal is to control a snake to move and collect food in a map.

## SWOP

### strength

- Well making games is not really that easy. First of all one must have a good grip over the basics. Logic building and program analysis plays a key role.
	- First of all draft a basic plot what you really want the game should be like.
	- Start with how to make the game go on until its over ? how to animate the motion of snake on your screen ? MOST IMP. what are the dimensions for your plot , length of snake , the dimensions of point its gonna grasp etc.
	- Now decide the keys user will be using for motion of snake like move up , move down , move right and move left. Until snake changes its direction it continues to move in that direction. Animate the motion of snake in coordination with the key controls.
	- After designing the snake and boundaries of your plot. Go for collision detection like when the snake reaches this much value of boundary - BOOM Game Over!
	- You can also have a count on number of points collected by a snake using counter like countPoints.

### Weakness

- The present implementation of iSnake can only be played in LAN. Due to large latency time and bandwidth limitation, it cannot be played over the Internet.
- Path finding algorithms (Blackmamba and Viper) implemented in this game have their own computation limitations which has been described in ANNEX A and B of the project report.
- Full stress test of the application has not been done yet. Hence, the response of game server in unpredictable situations cannot be handled properly.

### Oppurtunity

- C programming has a very good career like opportunities in different field like robotics, Artificial intelligence, machine learning, etc. The C programmers not only work in the field of computer only, but they can also pursue their career in Education, teaching, Government sectors, etc.

### Threads

- In the client side of the system, there are in total 2 threads, including the main thread, as seen in below. Note that these threads do not share data and thus no locks were required.

- Thread 1: This thread creates the TCP/IP server that accepts any address. If the server was created successfully, the server will listen for any clients otherwise exits the program. Whenever a client is accepted by the server, another thread is created to handle the new connection and the server thread continues to listen for other connections. This thread can create many child threads and therefore the server is capable of handling multiple requests from different clients simultaneously.

- Thread 3-many: These threads are created by the server to handle a new connection so that the server can be left listening to other connections. Whenever this thread is created, it determine the initial positions of the snakes where there are no other snakes/foods on. The snake, the socket file descriptor and a unique ID to the client used are saved inside a struct and the struct is saved inside a vector. Afterwards, all the snakes and foods positions are re-sent by the thread to all clients to inform another player joined the game and give the new player the current map. Note that this thread only sends data one time, it is deleted shortly after. When the snake is determining the new position and adding the item to the vector, the vector is locked using a mutex lock to prevent other threads from accessing the vector.

- Thread 2: The job of this thread is to be the game manager. It creates Thread 4 and Thread 5 which are needed for the game. If the thread creation was successful, this thread will handle the movements of all snakes periodically. When there is a movement action, all snakes will move. There are 4 conditions the thread check for every snake.

- If the next position results in two snakes colliding head-to-head, both snakes will die. All clients are informed with the dead.

- If the next position results in the snake colliding with another snake or with the game border, the snake will die. All clients are informed with the dead.

- If the next position results in a location of a food, the snake will grow and move afterwards. If the snake reaches the winning size, all clients are informed with the win and restarts the game. Note that there could be multiple winners. The thread will also send the foods positions to all clients to inform that the food was eaten.

- If nothing from above occured, move all positions of the snake to the new positions. Clients are informed with all the new snakes positions. Before using and updating the snakes, a lock is used. Other threads can add or remove items from the vectors used and thus could cause trouble when updating the snake. Since lock is used, the thread was kept single threaded (instead of having a thread for every snake) since other threads would need to wait for the lock to be unlocked.

- Thread 4: The thread manages the creation of foods. For every random interval a food is generated at a random location which is empty. When a food is generated, all food positions are sent to all clients. A lock is used every time a food needs to be created since it needs to check positions to ensure it is not taken.

- Thread 5: This thread reads the new direction of the snake sent from the client. To handle multiple clients, the socket was temporary switched to non-blocking instead blocking thus the read function will not wait for data to be received, an error will be shown instead. This error can be read and ignore if it matches that no data was found in the socket. Whenever the threads need to change the direction of a snake, a lock is used to ensure that the change will not effect the movement action.

## WWWH

### Who invented that
- It was programmed in 1997 by Taneli Armanto of Nokia and introduced on the Nokia 6110. Snake II – Included on monochrome phones such as the Nokia 3310 from 2000

### What is this game
- The game involves controlling a single block or snakehead by turning only left or right by ninety degrees until you manage to eat an apple. When you get the apple, the Snake grows an extra block or body segment. If, or rather when, the snake bumps into the edge of the screen or accidentally eats himself the game is over. The more apples the snake eats the higher the score

### where we can find
- It was sold under numerous names and many platforms but probably gained widespread recognition when it was shipped as standard on Nokia mobile phones in the late 1990's.

### How it works
- The player controls a dot, square, or object on a bordered plane. As it moves forward, it leaves a trail behind, resembling a moving snake. In some games, the end of the trail is in a fixed position, so the snake continually gets longer as it moves.

## Detailed Requirements

- Snake Classic System Requirements - full specs, system checker and the gaming PC setup you need.
- Snake Classic recommended requirements
- Memory: 4 GB
- Graphics Card: ATI FireGL T2-128
- CPU: Intel Pentium 4 2.00GHz
- File Size: 20 MB
- OS: Windows 7/8/10
- Snake Classic minimum requirements
- Memory: 4 GB
- Graphics Card: ATI FireGL T2-128
- CPU: Intel Pentium 4 2.00GHz
- File Size: 20 MB
- OS: windows 7/8/10
- Automatically test your computer against Snake Classic system requirements. Check if your PC can run the game with our free, easy-to-use detection tool or enter your system manually.
