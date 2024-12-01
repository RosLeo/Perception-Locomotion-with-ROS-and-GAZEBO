# **Perception & Locomotion**

## **Project Description**
This project implements a basic version of the **"see-think-act"** cycle using ROS (Robot Operating System). The goal is to design and control a mobile robot that autonomously moves to chase a ball in a simulated environment using RGB camera perception and motion control.

---

## **Objective**
The robot follows the "see-think-act" cycle:
1. **See**: Uses an RGB camera to perceive the environment and identify a ball (through color detection).
2. **Think**: Calculates the necessary movement to approach the ball (determining linear and angular velocities).
3. **Act**: Sends movement commands to the motors to head toward the ball.

---

## **Project Structure**
The project is organized as a ROS workspace with two main packages:
### **1. `ball_chaser` Package**
- Contains the nodes and services to control the robot’s movement toward the ball.
- **Main files**:
  - `drive_bot.cpp`: Sends movement commands based on the ball's coordinates.
  - `process_image.cpp`: Processes the camera image to detect the ball's position.
  - `DriveToTarget.srv`: A ROS service that accepts linear and angular velocity commands.

### **2. `my_robot` Package**
- Contains the robot description (URDF) and the simulated world configuration.
- **Main files**:
  - `my_robot.xacro`: The robot model (differential drive with a mounted camera).
  - `andrews.world`: The simulated environment in Gazebo where the ball is located.

---

## **"See-Think-Act" Cycle Implementation**

### **1. See (Perception)**
- **RGB Sensor**:
  - The robot uses an RGB camera to capture images of the environment.
  - The `process_image` node:
    - Subscribes to the camera topic (`/camera/rgb/image_raw`).
    - Processes each image to detect a specific color (the ball’s color).
    - Identifies the ball's position in the image pixels (left, right, center).

### **2. Think (Processing)**
- **Movement Command Calculation**:
  - If the ball is in the center of the image: The robot moves straight forward.
  - If the ball is on the right or left: The robot rotates to center it.
  - If the ball is not visible: The robot stops or searches for the ball.

### **3. Act (Action)**
- **Movement Commands**:
  - The `drive_bot` node sends velocity commands to the `/mobile_base_controller/cmd_vel` topic.
  - Publishes `geometry_msgs/Twist` messages with:
    - Linear velocity (`linear_x`) to move toward the ball.
    - Angular velocity (`angular_z`) to rotate and center the ball.

---

## **Key Files and Components**
- **`process_image` Node**:
  - Processes the RGB image to locate the ball.
  - Calls the `DriveToTarget` service to set the robot’s velocities.
- **`drive_bot` Node**:
  - Implements the `DriveToTarget` service.
  - Converts requested velocities into motor commands.
- **`DriveToTarget` Service**:
  - Accepts linear and angular velocity inputs and controls the robot's movement.
- **Gazebo Simulation**:
  - Launches a 3D world with the robot and the ball placed in a specific area.

---

## **Required Knowledge**
- **Sensors**: Understanding RGB camera functionality and `sensor_msgs/Image` messages.
- **ROS**:
  - Organizing workspaces and packages.
  - Creating nodes, services, and launch files.
  - Communicating via topics and services.
- **Gazebo**:
  - Configuring simulated environments and robot models.
- **C++/Python**: Writing ROS nodes.

---

## **Future Applications**
- Enhance detection using advanced techniques (e.g., Deep Learning for object classification).
- Implement mapping and localization (SLAM) for more sophisticated tracking.
- Navigate the robot in more complex environments with obstacles.

---

# **Perception & Locomotion**

## **Descrizione del Progetto**
Questo progetto implementa una versione base del ciclo **"see-think-act" (osserva-pensa-agisci)** utilizzando ROS (Robot Operating System). L'obiettivo è progettare e controllare un robot mobile che si muove autonomamente per inseguire una palla in un ambiente simulato, utilizzando la percezione tramite telecamere RGB e il controllo del movimento.

---

## **Obiettivo**
Il robot segue il ciclo "see-think-act":
1. **See (Vedi)**: Utilizza una telecamera RGB per percepire l'ambiente e identificare una palla (attraverso la rilevazione del colore).
2. **Think (Pensa)**: Calcola il movimento necessario per avvicinarsi alla palla (determinando velocità lineare e angolare).
3. **Act (Agisci)**: Invia comandi di movimento ai motori per dirigersi verso la palla.

---

## **Struttura del Progetto**
Il progetto è organizzato come workspace ROS con due pacchetti principali:
### **1. Pacchetto `ball_chaser`**
- Contiene i nodi e i servizi per controllare il movimento del robot verso la palla.
- **File principali**:
  - `drive_bot.cpp`: Invoca comandi di movimento basati sulle coordinate della palla.
  - `process_image.cpp`: Analizza l'immagine della telecamera per identificare la posizione della palla.
  - `DriveToTarget.srv`: Un servizio ROS che accetta comandi di velocità lineare e angolare.

### **2. Pacchetto `my_robot`**
- Contiene la descrizione del robot (URDF) e la configurazione del mondo simulato.
- **File principali**:
  - `my_robot.xacro`: Modello del robot (differential drive con una telecamera montata).
  - `andrews.world`: Ambiente simulato in Gazebo dove si trova la palla.

---

## **Ciclo "See-Think-Act" Implementato**

### **1. See (Percezione)**
- **Sensore RGB**:
  - Il robot utilizza una telecamera RGB per acquisire immagini dell'ambiente.
  - Il nodo `process_image`:
    - Sottoscrive i messaggi del topic della telecamera (`/camera/rgb/image_raw`).
    - Analizza ogni immagine per rilevare un colore specifico (quello della palla).
    - Identifica la posizione della palla nei pixel dell'immagine (destra, sinistra, centro).

### **2. Think (Elaborazione)**
- **Calcolo dei comandi di movimento**:
  - Se la palla è nel centro dell'immagine: Il robot si muove dritto.
  - Se la palla è sulla destra o sinistra: Il robot ruota per centrarla.
  - Se la palla non è visibile: Il robot si ferma o cerca la palla.

### **3. Act (Azione)**
- **Comandi di movimento**:
  - Il nodo `drive_bot` invia comandi di velocità al topic `/mobile_base_controller/cmd_vel`.
  - Pubblica messaggi di tipo `geometry_msgs/Twist` con:
    - Velocità lineare (`linear_x`) per avvicinarsi alla palla.
    - Velocità angolare (`angular_z`) per ruotare e centrare la palla.

---

## **File e Componenti Chiave**
- **Nodo `process_image`**:
  - Analizza l'immagine RGB per localizzare la palla.
  - Richiede il servizio `DriveToTarget` per impostare le velocità del robot.
- **Nodo `drive_bot`**:
  - Implementa il servizio `DriveToTarget`.
  - Converte le velocità richieste in comandi per i motori.
- **Servizio `DriveToTarget`**:
  - Accetta input di velocità lineare e angolare e controlla il movimento del robot.
- **Simulazione Gazebo**:
  - Lancia un mondo 3D con il robot e la palla posizionata in un'area specifica.

---

## **Conoscenze Richieste**
- **Sensoristica**: Comprendere il funzionamento delle telecamere RGB e dei messaggi `sensor_msgs/Image`.
- **ROS**:
  - Organizzazione di workspace e pacchetti.
  - Creazione di nodi, servizi e file di lancio.
  - Comunicazione tramite topic e servizi.
- **Gazebo**:
  - Configurazione di ambienti simulati e modelli di robot.
- **C++/Python**: Per scrivere i nodi ROS.

---

## **Applicazioni Future**
- Migliorare il rilevamento usando tecniche avanzate (ad esempio, Deep Learning per la classificazione degli oggetti).
- Implementare una mappa e localizzazione (SLAM) per un inseguimento più sofisticato.
- Controllare il robot in ambienti più complessi con ostacoli.



