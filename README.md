# turtlesim_catch_them_all
🐢 Turtle Catcher – Autonomous Turtle Hunting using ROS 2
📌 Overview

Turtle Catcher is a ROS 2 project developed using Python (rclpy) and Turtlesim that demonstrates autonomous robot navigation, inter-node communication, and service-based task execution. The project consists of two ROS 2 nodes that work together to spawn turtles randomly in the simulation and automatically navigate the main turtle (turtle1) to catch them.

The system makes use of Publishers, Subscribers, Timers, Parameters, Custom Messages, and Custom Services, providing a complete example of how multiple ROS 2 nodes can cooperate to perform autonomous tasks.

🚀 Features
🐢 Random spawning of turtles inside the Turtlesim environment.
🎯 Autonomous navigation of the main turtle toward target turtles.
📍 Option to prioritize the closest turtle or follow the order of spawning.
📡 Real-time publishing of all alive turtles.
⚙️ Configurable spawning frequency and turtle naming.
🔄 Asynchronous service communication for catching turtles.
🧩 Uses custom ROS 2 messages and services.
💻 Fully developed using ROS 2 Python (rclpy).

🏗️ System Architecture
                     +----------------------+
                     |  Turtle Spawner Node |
                     +----------------------+
                               |
                 Publishes Alive Turtles
                               |
                      /alive_turtles Topic
                               |
                               ▼
                  +-------------------------+
                  | Turtle Controller Node  |
                  +-------------------------+
                               |
                  Subscribes to Turtle Pose
                               |
                               ▼
                 Calculates Target Turtle
                               |
                               ▼
             Publishes Velocity Commands
                    /turtle1/cmd_vel
                               |
                               ▼
                     Turtle reaches target
                               |
                               ▼
                 Calls Catch Turtle Service
                               |
                               ▼
                  Turtle Spawner removes turtle
                  
📂 Project Structure
turtle_catcher/
│
├── turtle_controller.py
├── turtle_spawner.py
│
├── msg/
│   ├── Turtle.msg
│   └── TurtleArray.msg
│
└── srv/
    └── CatchTurtles.srv
    
⚙️ How It Works
1️⃣ Turtle Spawner Node
The Turtle Spawner node is responsible for generating turtles at random positions inside the simulator.
Responsibilities
Creates turtles at configurable intervals.
Assigns unique names to each turtle.
Maintains a list of alive turtles.
Publishes the list using a custom message.
Hosts the custom catch_turtle service.
Removes turtles when requested by the controller.

2️⃣ Turtle Controller Node
The Turtle Controller node acts as the autonomous robot controller.
Responsibilities
Reads the current pose of turtle1.
Receives all alive turtles.
Chooses the target turtle.
Calculates distance and heading.
Drives the turtle using velocity commands.
Calls the custom service once the turtle is reached.

📡 ROS 2 Communication
Publishers
Topic	Description
/turtle1/cmd_vel	Controls turtle movement
/alive_turtles	Publishes all currently alive turtles
Subscribers
Topic	Description
/turtle1/pose	Current position of turtle1
/alive_turtles	Receives spawned turtle information
Services
Service	Purpose
/spawn	Creates new turtles
/kill	Removes turtles
/catch_turtle	Custom service to catch a turtle

⚙️ Parameters
Turtle Controller
Parameter	Default	Description
catch_closest_turtle_first	true	Catch the nearest turtle instead of the oldest one
Turtle Spawner
Parameter	Default	Description
spawn_frequency	1.0	Number of turtles spawned every second
turtle_name_prefix	"turtle"	Prefix for spawned turtle names

🧠 Navigation Logic
The controller continuously performs the following steps:
Wait for the turtle's current pose.
Receive the list of alive turtles.
Select the target turtle.

Compute:
Distance
Desired heading
Rotate toward the target.
Move forward.
Stop near the turtle.
Call the custom catch service.
Repeat until all turtles are removed.

🛠️ Technologies Used
ROS 2
Python (rclpy)
Turtlesim
Custom Messages
Custom Services
Geometry Messages
Timers
Parameters
Asynchronous Service Calls

🎯 Learning Outcomes
This project demonstrates practical use of:
ROS 2 Nodes
Publisher–Subscriber communication
Client–Server architecture
Custom interfaces
Motion control
Robot navigation
Parameter management
Timer-based execution
Multi-node coordination
Modular ROS 2 application development

📈 Future Improvements
PID-based velocity controller
Dynamic obstacle avoidance
Multi-robot turtle catcher
Action Server implementation
RViz visualization
Gazebo integration
Score tracking
Path planning algorithms
Graphical dashboard for monitoring

▶️ Expected Output
When the project starts, turtles are spawned randomly across the Turtlesim window. The main turtle (turtle1) automatically detects the target turtle, navigates toward it using calculated linear and angular velocities, and requests its removal through a custom ROS 2 service once it reaches the target. This process repeats continuously, creating an autonomous turtle-catching system that showcases coordinated communication between multiple ROS 2 nodes.
When the project starts, turtles are spawned randomly across the Turtlesim window. The main turtle (turtle1) automatically detects the target turtle, navigates toward it using calculated linear and angular velocities, and requests its removal through a custom ROS 2 service once it reaches the target. This process repeats continuously, creating an autonomous turtle-catching system that showcases coordinated communication between multiple ROS 2 nodes.
