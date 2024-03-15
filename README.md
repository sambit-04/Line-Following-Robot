
# Arduino Line Following Robot: Autonomous Path Tracking with Infrared Sensors

This Arduino code facilitates the operation of a Line Following Robot, which relies on infrared sensors to detect a predefined path. By interpreting sensor data, the robot dynamically adjusts its motor movements to effectively stay on course. This functionality serves educational purposes, offering insights into robotics principles, while also presenting practical utility in automated navigation scenarios such as warehouse logistics or assembly line operations.


## Features


Key features of this Line Following Robot project include:

- Autonomous navigation: The robot can follow a predefined path or line without human intervention.
- Infrared sensing: Utilizes infrared sensors to detect the line on the surface, allowing for real-time adjustments in movement.
- Directional control: Capable of making turns and adjusting speed based on sensor readings to stay on course.
- Versatility: Can be adapted for various line-following applications, such as maze-solving or automated transportation.
- Educational value: Provides a hands-on learning experience in robotics, coding, and sensor integration for enthusiasts and students.
- Scalability: Can serve as a foundation for more complex robotics projects by integrating additional sensors or functionalities.
- Open-source: Utilizes Arduino platform and C++ programming language, enabling easy customization and modification by the community.
- Integration potential: Can be integrated with other hardware and software systems for enhanced functionality, such as wireless communication or obstacle avoidance.

## Working

As stated earlier, line follower robot (LFR) follows a line, and in order to follow a line, robot must detect the line first. Now the question is how to implement the line sensing mechanism in a LFR. We all know that the reflection of light on the white surface is maximum and minimum on the black surface because the black surface absorbs maximum amount of light. So, we are going to use this property of light to detect the line. To detect light, either LDR (light-dependent resistor) or an IR sensor can be used. For this project, we are going with the IR sensor because of its higher accuracy. To detect the line, we place two IR sensors one on the left and other on the right side of the robot as marked in the diagram below. We then place the robot on the line such that the line lies in the middle of both sensors. We have covered a detailed Arduino IR sensor tutorial which you can check to learn more about the working of IR sensors with Arduino Uno.

Infrared sensors consist of two elements, a transmitter and a receiver. The transmitter is basically an IR LED, which produces the signal and the IR receiver is a photodiode, which senses the signal produced by the transmitter. The IR sensors emits the infrared light on an object, the light hitting the black part gets absorbed thus giving a low output but the light hitting the white part reflects back to the transmitter which is then detected by the infrared receiver, thereby giving an analog output. Using the stated principle, we control the movement of the robot by driving the wheels attached to the motors, the motors are controlled by a microcontroller.

## Navigation

A typical line follower robot has two sets of motors, let's call them left motor and right motor. Both motors rotate  on the basis of the signal received from the left and the right sensors respectively. The robot needs to perform 4 sets of motion which includes moving forward, turning left, turning right and coming to a halt. The description about the cases are given below.

**Moving Forward:**

![App Screenshot](https://circuitdigest.com/sites/default/files/inlineimages/u3/Line-Follower-Navigation.jpg)

In this case, when both the sensors are on a white surface and the line is between the two sensors, the robot should move forward, i.e., both the motors should rotate such that the robot moves in forward direction (actually both the motors should rotate in the opposite direction due to the placement of motors in our setup. But for the sake of simplicity, we will call the motors rotating forward.)

**Turning LEFT:**

![App Screenshot](https://circuitdigest.com/sites/default/files/inlineimages/u3/Line-Follower-Left-Navigation.png)

In this case, the left sensor is on top of the dark line, whereas the right sensor is on the white part, hence the left sensor detects the black line and gives a signal, to the microcontroller. Since, signal comes from the left sensor, the robot should turn to the left direction. Therefore, the left motor rotates backwards and the right motor rotates in forward direction. Thus, the robot turns towards left side.

**Turning RIGHT:**

![App Screenshot](https://circuitdigest.com/sites/default/files/inlineimages/u3/Line-Follower-Right-Navigation.png)

This case is similar to the left case, but in this situation only the right sensor detects the line which means that the robot should turn in the right direction. To turn the robot towards the right direction, the left motor rotates forward and the right motor rotates backwards and as a result, the robot turns towards the right direction.

**Stopping:**

![App Screenshot](https://circuitdigest.com/sites/default/files/inlineimages/u3/Line-Follower-STOP-Navigation.png)

In this case, both the sensors are on top of the line and they can detect the black line simultaneously, the microcontroller is fed to consider this situation as a process for halt. Hence, both the motors are stopped, which causes the robot to stop moving.
## Tech Stack & Components Required:

**Software:**
- The programming language used in this project is C++, specifically the Arduino variant of C++ for microcontroller programming.
- Arduino IDE for coding and uploading the firmware to the Arduino microcontroller board.

**Hardware:**
- Arduino microcontroller board (e.g., Arduino Uno)
- L293D motor driver for controlling the DC motors
- Infrared sensors (R_S and L_S) for detecting the line on the surface
- DC motors for driving the robot's movement
- Other necessary electronic components such as resistors, jumper wires, and a power source.

In addition to the software and hardware components, the main body of the robot typically includes:

- Chassis: The frame or base of the robot where all components are mounted.
- Wheels: Attached to the DC motors to provide movement.
- Motor mounts: Structures to securely hold the DC motors in place on the chassis.
- Sensor mounts: Mounting brackets or holders for positioning the infrared sensors at the appropriate angle and distance from the surface.
- Battery holder: To provide power to the Arduino board, motor driver, and motors.
- Breadboard or PCB (Printed Circuit Board): Used for prototyping and organizing the electrical connections.
- Fasteners: Screws, nuts, bolts, or other hardware to assemble the chassis and mount components securely.

These components are assembled together to create a robust and functional platform for the Line Following Robot.

![App Screenshot](https://circuitdigest.com/sites/default/files/inlineimages/u3/Line-Follower-Robot-Components.jpg)

## Circuit Diagram

![App Screenshot](https://circuitdigest.com/sites/default/files/circuitdiagram_mic/Line-Follower-Circuit-Diagram.png)

The circuit consists of mainly four parts: Two IR sensors, one motor drive, two motors, one Arduino, a battery and few connecting wires. The sensor senses the IR light reflected from the surface and feeds the output to the onboard op-amp comparator. When the sensor is situated over the white background, the light emitted by the sensor is reflected by the white ground and is received by the receiver. But when the sensor is above the black background, the light from the source doesn’t reflect to it. The sensor senses the intensity of reflected light to give an output. The sensor’s output is fed to the microcontroller, which gives commands to the motor driver to drive the motor accordingly. In our project, the Arduino Uno is programmed to make the robot move forward, turn right or turn left and stop according to the input coming from the sensor. The output of the Arduino is fed to the motor driver.
** **


**Why We Require a Motor Driver?**

The reason to use a motor driver here is because the output signal of an Arduino is not sufficient to drive the motor, furthermore, we need to rotate the motors in both directions, therefore we use a motor driver to drive the motor as required and also the motor driver is able to supply sufficient current to drive the motor. Here, we are using a L293D motor driver which is a dual h bridge motor driver and is sufficient for our 2 motors.

The L293D has 16 pins, the pinout of L293D is shown in the below diagram.

![App Screenshot](https://circuitdigest.com/sites/default/files/inlineimages/u3/L293D-Pinout.png)

**Connection of motor driver pins are as follows:**

Pin number 1 and 9 are the enable pins, we connect these two pins to a 5v input to enable the motor.

Pin number 1A, 2A, 3A, and 4A are the control pins.

For eg. The motor will turn to the right if the pin 1A goes low and 2A goes high, and the motor will turn to the left if 1A goes low and 2A high. So, we connect these pins to the output pins of the decoder.

Pins 1Y, 2Y, 3Y, and 4Y are the motor connection pins.

Note: Vcc2 is the motor driving voltage pin, and only used if you are using a high voltage motor.

**Pin connection of Arduino Uno with the Motor driver are as follows:**

![App Screenshot](https://circuitdigest.com/sites/default/files/inlineimages/u3/Motor-Driver-and-Arduino-Connections.png)

Here, we are using a 7.4 li-ion battery to power the whole circuit. You can use any battery type from 6-12 volt. To move the robot, we need to use motors with low RPM but torque high enough to carry the weight of the robot. So, I chose two 60 RPM 6V Battery Operated, geared motors for this robot.
## Assembling the Line Follower Robot

Once we have understood the connection of all the components, we can start assembling our LFR.

![App Screenshot](https://circuitdigest.com/sites/default/files/inlineimages/u3/Line-Follower-Robot-using-Arduino.jpg)

To make this robot, first we need a robot body; here I am using a homemade chassis. You can either use a readymade chassis or build one yourself.

Now, place the BO motors to the chassis with the help of some hot glue as shown in the image below. 

![App Screenshot](https://circuitdigest.com/sites/default/files/inlineimages/u3/Line-Follower-Motor-Assembly.png)

Next step is to place the motor driver on chassis and connect the motor wires to the output of the motor driver.

Next, bend the IR LED and sensor as shown in the image.

![App Screenshot](https://circuitdigest.com/sites/default/files/inlineimages/u3/IR-LED-Sensor.png)

Then place the sensors on the downside of the robot, adjust the sensors according to the track width and robot width. Remember that one sensor is for left side detection and another is for the right side detection.

![App Screenshot](https://circuitdigest.com/sites/default/files/inlineimages/u3/Line-Follower-Robot-Assembly.jpg)

Now place the Arduino uno using glue and connect the sensor output pins to digital pin 2 and 4 of the Arduino.

![App Screenshot](https://circuitdigest.com/sites/default/files/inlineimages/u3/Line-Follower-Robot.jpg)

Connect the VCC pins to 5volt and the ground pins to ground.

Now, connect the enable pins of the motor driver to pin 5 and 8 of Arduino and connect the motor driver input pins to pin number 6, 7, 9 and 10 of Arduino respectively.

Finally, connect the battery with the circuit and place the battery on chassis. Here, I have connected everything with jumper wires. To make a permanent setup, you can directly solder everything together.

Now turn the board upside down and with the help of hot glue gun, attach the castor wheels as shown in the image below.

![App Screenshot](https://circuitdigest.com/sites/default/files/inlineimages/u3/Line-Follower-Chasis-Board.jpg)

Finally, add the wheels. For extra safety, I have added a plastic sheet as a bumper too.

![App Screenshot](https://circuitdigest.com/sites/default/files/inlineimages/u3/Arduino%20Line%20Follower.jpg)
## Installation

To install and run this code for the Line Following Robot:

1. **Install Arduino IDE**: If you haven't already, download and install the Arduino IDE from the official Arduino website (https://www.arduino.cc/en/software).

2. **Connect Arduino Board**: Connect your Arduino board (e.g., Arduino Uno) to your computer using a USB cable.

3. **Open Arduino IDE**: Open the Arduino IDE software on your computer.

4. **Copy and Paste Code**: Copy the provided Arduino code for the Line Following Robot and paste it into a new sketch in the Arduino IDE.

5. **Verify and Upload**: Click on the "Verify" button (checkmark icon) to compile the code and check for any errors. If no errors are reported, click on the "Upload" button (right arrow icon) to upload the code to your Arduino board.

6. **Connect Components**: Make sure to connect the hardware components according to the pin configurations specified in the code. This includes connecting the motors, infrared sensors, and motor driver to the appropriate pins on the Arduino board.

7. **Power Up**: Power up your Line Following Robot by connecting a suitable power source (e.g., battery pack) to the Arduino board and ensuring all connections are secure.

8. **Test**: Place the robot on a surface with a marked path or line and observe its behavior. The robot should autonomously follow the line based on the sensor readings and motor control.

Following these steps will enable you to successfully install and run the provided code for your Line Following Robot project.
## Testing and Calibration

![Line Follower Robot Circuit Demo](https://circuitdigest.com/sites/default/files/inlineimages/u3/Line-Follower-Robot-Project.jpg)

We have assembled the robot and uploaded the code, so now its time to see it in action and if it is unable to follow the line then we’ll have to calibrate the robot. For that first place robot on a  black surface ( both sensors should be on top of the black surface) then adjust the variable resistor of IR Module until the output led of IR module become off. Next, place the robot on a white surface and check whether the led is turning on, if not, then just adjust the variable resistor. Repeat the process once again to be sure that the output LED is operating as per the requirement.

Now, since we have calibrated the robot, all we need to do is place the robot on top of the black line and see it in action.

![Line Follower Robot Circuit Demo](https://circuitdigest.com/sites/default/files/inlineimages/u3/Line-Follower.gif)
## Screenshots

![App Screenshot](https://circuitdigest.com/sites/default/files/inlineimages/u3/Line-Follower-Robot-Components.jpg)

![App Screenshot](https://circuitdigest.com/sites/default/files/inlineimages/u3/Arduino%20Line%20Follower.jpg)

![App Screenshot](https://circuitdigest.com/sites/default/files/inlineimages/u3/Line-Follower-Robot-Project.jpg)

## Authors

- [@sambit-04 (Sambit Mazumder)](https://github.com/sambit-04)
- [@Siddhesh-96 (Siddhesh Mane)]([https://github.com/sambit-04](https://github.com/Siddhesh-96))


## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details. Feel free to use, modify, and distribute the code for your own projects.


## Acknowledgements

 - [Circuit Digest](https://circuitdigest.com/)

Special thanks to CircuitDigest.com for providing valuable resources and tutorials that contributed to the development of this Line Following Robot project. Their insightful articles and guides helped in understanding the fundamentals of robotics and Arduino programming, making this project possible.


