🚗 Arduino Bluetooth Controlled Car Project 🔵
Excited to share our recent project: Arduino Bluetooth Controlled Car with Front & Back Lights 💡
🔧 Project Overview
We built a wireless car controlled via Bluetooth using a smartphone app. The system is powered by Arduino UNO and the HC-05 Bluetooth module, making it perfect for beginners in embedded systems.
⚙️ Key Features
✔️ Forward, backward, left, right movement
✔️ Smooth directional control (top-left, top-right, etc.)
✔️ Front (white LED) & back (red LED) lights
✔️ Real-time Bluetooth control via mobile app
🧩 Components Used
Arduino UNO
HC-05 Bluetooth Module
L293D Motor Driver
TT Gear Motors (4x)
LEDs with resistors
18650 Batteries
Custom chassis & wheels
💻 Technology & Logic
Programming Language: C/C++ (Arduino IDE)
Serial communication at 9600 baud rate
Command-based control system (F, B, L, R, etc.)
🚧 Challenges We Faced
Loose motor connections → solved with proper soldering
LED overheating → added resistors
Bluetooth pairing issues → fixed via correct wiring & baud rate
🎯 Outcome
Successfully developed a fully functional Bluetooth-controlled car with lighting system — a great hands-on experience in robotics and embedded systems!

💻 Code Implementation
#include <AFMotor.h>
//initial motors pin
AF_DCMotor motor1(1, MOTOR12_1KHZ);
AF_DCMotor motor2(2, MOTOR12_1KHZ);
AF_DCMotor motor3(3, MOTOR34_1KHZ);
AF_DCMotor motor4(4, MOTOR34_1KHZ);
int val;
int Speeed = 255;
void setup()
{Serial.begin(9600); //baud rate}
void loop(){
  if(Serial.available() > 0){
    val = Serial.read();
    Stop(); //initialize w motors stoped
          if (val == 'F'){forward();}
          if (val == 'B'){back();}
          if (val == 'L'){left();}
          if (val == 'R'){right();}
          if (val == 'I'){topright();}
          if (val == 'J'){topleft();}
          if (val == 'K'){bottomright();}
          if (val == 'M'){bottomleft();}
          if (val == 'T'){Stop();}
  }
}
void forward()
{
  motor1.setSpeed(Speeed);
  motor1.run(FORWARD);
  motor2.setSpeed(Speeed); 
  motor2.run(FORWARD); 
  motor3.setSpeed(Speeed);
  motor3.run(FORWARD); 
  motor4.setSpeed(Speeed);
  motor4.run(FORWARD); 
}
 
void back()
{
  motor1.setSpeed(Speeed);
  motor1.run(BACKWARD);
  motor2.setSpeed(Speeed); 
  motor2.run(BACKWARD); 
  motor3.setSpeed(Speeed); 
  motor3.run(BACKWARD); 
  motor4.setSpeed(Speeed); 
  motor4.run(BACKWARD); 
}
void left()
{
  motor1.setSpeed(Speeed); 
  motor1.run(BACKWARD); 
  motor2.setSpeed(Speeed); 
  motor2.run(BACKWARD); 
  motor3.setSpeed(Speeed); 
  motor3.run(FORWARD);  
  motor4.setSpeed(Speeed); 
  motor4.run(FORWARD);  
}
 
void right()
{
  motor1.setSpeed(Speeed); 
  motor1.run(FORWARD); 
  motor2.setSpeed(Speeed); 
  motor2.run(FORWARD); 
  motor3.setSpeed(Speeed); 
  motor3.run(BACKWARD); 
  motor4.setSpeed(Speeed); 
  motor4.run(BACKWARD); 
}
void topleft(){
  motor1.setSpeed(Speeed); 
  motor1.run(FORWARD); 
  motor2.setSpeed(Speeed); 
  motor2.run(FORWARD); 
  motor3.setSpeed(Speeed/3.1);
  motor3.run(FORWARD); 
  motor4.setSpeed(Speeed/3.1);
  motor4.run(FORWARD); 
}
 
void topright()
{
  motor1.setSpeed(Speeed/3.1); 
  motor1.run(FORWARD); 
  motor2.setSpeed(Speeed/3.1); 
  motor2.run(FORWARD); 
  motor3.setSpeed(Speeed);
  motor3.run(FORWARD); 
  motor4.setSpeed(Speeed);
  motor4.run(FORWARD); 
}
void bottomleft()
{
  motor1.setSpeed(Speeed); 
  motor1.run(BACKWARD); 
  motor2.setSpeed(Speeed); 
  motor2.run(BACKWARD); 
  motor3.setSpeed(Speeed/3.1); 
  motor3.run(BACKWARD); 
  motor4.setSpeed(Speeed/3.1); 
  motor4.run(BACKWARD); 
}
 
void bottomright()
{
  motor1.setSpeed(Speeed/3.1); 
  motor1.run(BACKWARD); 
  motor2.setSpeed(Speeed/3.1); 
  motor2.run(BACKWARD); 
  motor3.setSpeed(Speeed); 
  motor3.run(BACKWARD); 
  motor4.setSpeed(Speeed); 
  motor4.run(BACKWARD); 
}
void Stop()
{
  motor1.setSpeed(0); //Minimum velocity
  motor1.run(RELEASE); //stop the motor
  motor2.setSpeed(0); 
  motor2.run(RELEASE); 
  motor3.setSpeed(0); 
  motor3.run(RELEASE); 
  motor4.setSpeed(0); 
  motor4.run(RELEASE); 
}
