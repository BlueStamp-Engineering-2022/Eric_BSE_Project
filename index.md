# Color Candy Sorter (WEBSITE WIP, WILL FINISH BY SATURDAY (7/23) OR SUNDAY (7/24)
This will serve as a brief description of your project. Limit this to three sentences because it can become overly long at that point. This copy should draw the user in and make she/him want to read more.

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Eric Zhu | Carlmont High School| Electrical Engineering | Incoming Senior

![image](https://user-images.githubusercontent.com/107578591/174335797-80d5601a-d719-45d7-a10f-01ea3ed9bb18.png)
  
# Final Milestone
My final milestone is the increased reliability and accuracy of my robot. I ameliorated the sagging and fixed the reliability of the finger. As discussed in my second milestone, the arm sags because of weight. I put in a block of wood at the base to hold up the upper arm; this has reverberating positive effects throughout the arm. I also realized that the forearm was getting disconnected from the elbow servo’s horn because of the weight stress on the joint. Now, I make sure to constantly tighten the screws at that joint. 

[![Final Milestone](https://res.cloudinary.com/marcomontalbano/image/upload/v1612573869/video_to_markdown/images/youtube--F7M7imOVGug-c05b58ac6eb4c4700831b2b3070cd403.jpg )](https://www.youtube.com/watch?v=F7M7imOVGug&feature=emb_logo "Final Milestone"){:target="_blank" rel="noopener"}

# Second Milestone
My final milestone is the increased reliability and accuracy of my robot. I ameliorated the sagging and fixed the reliability of the finger. As discussed in my second milestone, the arm sags because of weight. I put in a block of wood at the base to hold up the upper arm; this has reverberating positive effects throughout the arm. I also realized that the forearm was getting disconnected from the elbow servo’s horn because of the weight stress on the joint. Now, I make sure to constantly tighten the screws at that joint.

[![Second Milestone](https://res.cloudinary.com/marcomontalbano/image/upload/v1612574014/video_to_markdown/images/youtube--y3VAmNlER5Y-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=y3VAmNlER5Y&feature=emb_logo "Second Milestone"){:target="_blank" rel="noopener"}

# First Milestone
My first milestone was setting up and hooking up the Raspberry Pi and all the necessary components onto my tv. The heatsinks, the sd card, and the controller were all added to ensure that the Raspberry Pi was working. Instead of the Raspberry Pi Os software, I had to first download a different software called Retro Pie. With Retro Pie, I needed to download an Imager for Raspberry Pi. Raspberry Pi Imager automatically downloads a list of the latest versions of Raspbian supported by the Raspberry Pi. Raspbian is the typical Raspberry Pi Os software, the one I needed on the Raspberry Pi was Retro Pi. With the included SD card, I plugged in the SD into my computer and launched the Imager. The imager allowed me to set the Operating System to Retro Pi instead of Raspbian onto the SD card. With the OS imaged onto the SD, I plugged the SD card back into the Raspberry Pi and rebooted the system and Retro Bi booted up.

#include <Servo.h>

#define S0 2
#define S1 3
#define S2 4
#define S3 5
#define sensorOut 6

Servo topServo;
Servo bottomServo;

int frequency = 0;
int color =0;

void setup() {
  pinMode(S0, OUTPUT);
  pinMode(S1, OUTPUT);
  pinMode(S2, OUTPUT);
  pinMode(S3, OUTPUT);
  pinMode(sensorOut, INPUT);

  // Setting frequency-scaling to 20%
  digitalWrite(S0, HIGH);
  digitalWrite(S1, LOW);

  topServo.attach(7);
  bottomServo.attach(8);

  Serial.begin(9600);
}

void loop() {

  topServo.write(115);
  delay(500);

  for(int i = 115; i > 65; i--) {
    topServo.write(i);
    delay(2);
  }
  delay(500);

  color = readColor();
  delay(10);

  switch (color) {
    case 1:
    bottomServo.write(50);
    break;

    case 2:
    bottomServo.write(75);
    break;

    case 3:
    bottomServo.write(100);
    break;

    case 4:
    bottomServo.write(125);
    break;

    case 5:
    bottomServo.write(150);
    break;

    case 6:
    bottomServo.write(175);
    break;

    case 0:
    break;
  }
  delay (300);

  for(int i = 65; i > 29; i--) {
    topServo.write(i);
    delay(2);
  }
  delay(200);

  for(int i = 29; i < 115; i++) {
    topServo.write(i);
    delay(2);
  }
  color=0;
}

// Custom Function - readColor()
int readColor() {
  // Setting red filtered photodiodes to be read
  digitalWrite(S2, LOW);
  digitalWrite(S3, LOW);
  // Reading the output frequency
  frequency = pulseIn(sensorOut, LOW);
  int R = frequency;
  // Printing the value on the serial monitor
  Serial.print("R= ");//printing name
  Serial.print(frequency);//printing RED color frequency
  Serial.print("  ");
  delay(50);

  // Setting Green filtered photodiodes to be read
  digitalWrite(S2, HIGH);
  digitalWrite(S3, HIGH);
  // Reading the output frequency
  frequency = pulseIn(sensorOut, LOW);
  int G = frequency;
  
  // Printing the value on the serial monitor
  Serial.print("G= ");//printing name
  Serial.print(frequency);//printing RED color frequency
  Serial.print("  ");
  delay(50);

  // Setting Blue filtered photodiodes to be read
  digitalWrite(S2, LOW);
  digitalWrite(S3, HIGH);
  
  // Reading the output frequency
  frequency = pulseIn(sensorOut, LOW);
  int B = frequency;
  
  // Printing the value on the serial monitor
  Serial.print("B= ");//printing name
  Serial.print(frequency);//printing RED color frequency
  Serial.println("  ");
  delay(50);

  if(R<45 & R>32 & G<65 & G>55){
    color = 1; // Red
  }
  if(G<55 & G>43 & B<47 & B>35){
    color = 2; // Orange
  }
  if(R<53 & R>40 & G<53 & G>40){
    color = 3; // Green
  }
  if(R<38 & R>24 & G<44 & G>30){
    color = 4; // Yellow
  }
  if(R<56 & R>46 & G<65 & G>55){
    color = 5; // Brown
  }
  if (G<58 & G>45 & B<40 & B>26){
    color = 6; // Blue
  }
  return color;
}

![image](https://user-images.githubusercontent.com/107578591/175576848-e4e0d210-4385-40cb-bdcd-cf4f8c131cf1.png)

[![First Milestone](https://res.cloudinary.com/marcomontalbano/image/upload/v1612574117/video_to_markdown/images/youtube--CaCazFBhYKs-c05b58ac6eb4c4700831b2b3070cd403.jpg)](https://www.youtube.com/watch?v=CaCazFBhYKs "First Milestone"){:target="_blank" rel="noopener"}

# Useless Machine - Starter Project
My starter project was the useless machine. Essentially, it was a small black box that had a single lever on it. When you flip the lever, a little arm pops out of the top of the box and switched the lever back off. That's really all there is to it - it's a useless machine after all. Inside the box, there is a small circuit that connects a battery pack, a lever, some wires, and a motor. First, the battery pack is the power source of the entire contraption. When the lever is switched, it sends a signal through the circuit that turns on the motor. The motor is connected to the arm, so when it rotates, the arm moves. When the lever is switched off by the arm, the motor rotates in the opposite direction, thus returning the entire contraption back to the status quo. During my time assembling the useless machine, I ran into two primary issues. The first problem was that the motor arm was not moving at all when I switched teh leverl. This problem was solved after I realized the wires were poorly connected to the circuit. The other major problem that I encountered was screwing in the silicone box pillars. The lack of grip on the pillars coupled with tthe fact that they rotated when I tried screwing them in made the process difficult and tedious. Thankfully, wrapping a single rubberband around the pillars gave me enough grip and solved this issue. Overall, this project was quick, straight forward, fun, and most importantly, a good educational experience.

[![Starter Project](https://i3.ytimg.com/vi/lgbKN82H8b4/maxresdefault.jpg)](https://www.youtube.com/watch?v=lgbKN82H8b4)
