# Vihari's Gesture Controlled Car Portfolio
My project is a Gesture Controlled Car. This is essentially a remote control car, but instead of being controlled by a pair of joysticks, it is controlled with the movements of my hand. This is done with the use of something that many of us use everyday: bluetooth.

You should comment out all portions of your portfolio that you have not completed yet, as well as any instructions:
```HTML 
<!--- This is an HTML comment in Markdown -->
<!--- Anything between these symbols will not render on the published site -->
```

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Vihari T | Dougherty Valley High School | Computer Science | Incoming Senior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
# Final Milestone

**The next step was a modification. I wanted to put a robotic arm on top of the car and make that gesture controlled as well using a similar working to that of the car and controller.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/4Xq_3TuRaPQ?si=Hy1Auj6PlfsMPTbg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

-The first step towards this modification was to build the actual robotic arm itself. This was quite simple as I just followed a tutorial.
-The next step was to change the controls of the robotic arm, from the joysticks to the accelerometer. So I had to pair another two bluetooths that would make the Arduino Micro and the Nano board communicate. This was an issue as this meant I had to connect two bluetooth devices to the Arduino Micro. Initially I didn't think this was possible as the bluetooth just wouldn't connect to the Serial Port which was used to send messages. I fixed this problem by configuring the bluetooth while connecting it to the Nano and then just transferring the wiring over
-This was where I am at this point, but I hope to be able to alter the code uploaded into the arm to change the input of the if conditions from a joystick movement to an accelerometer reading



# Second Milestone

**After getting the controller working, I had to get the actual tires of the car rotating how I wanted them to.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/rMxV38q7EIY?si=lf3GS5kRRYRiGh00" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>

-The first thing I did was understand the workings of the h-bridge, and used two of them to control the right two and left two wheels. This was an issue as I needed the left two tires to move in synch with each other as well as the right two tires to move in synch with each other.
-By extending the connections of the h-bridge to a breadboard, I was able to synch up the right two and left two wheels. 
-I faced an issue after doing this, there wasn't enough power to rotate all the motors. I fixed this by plugging a 9V battery into the Arduino UNO
-Finally, I connected an accelerometer to the Arduino Micro, which is the controller of the car. An accelerometer is able to sense the tilt in itself and manifest that tilt as a number in the x or y direction. Then I programmed the Micro to be able to send over the readings on the accelerometer to the car. This made it so that the car would move in accordance to the tilt of the controller.

# First Milestone

**Getting the Bluetooths on the car and the controller to be synched was a challenging task for me who has never dealt with this kind of a project before. But eventually, I got it to work and completed the first step of this project.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/WXkEZ5nbTl8?si=fqcEhsrzOeRgtRXZ" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" referrerpolicy="strict-origin-when-cross-origin" allowfullscreen></iframe>


-The first step was to set up the wiring according to the wiring diagram. I kept messing this up because I kept confusing different wires and didn't understand how the breadboard worked, but eventually I got it wired properly.
-The next step was to understand what the code was actually doing. This wasn't too difficult as I just looked up all the syntax in the Arduino language references
-Finally, I had to configure the two bluetooths into a master and slave configuration. This took quite long as I kept messing up the AT commands which were involved with configuring the bluetooths, but I was successful after resetting the firmware and entering the commands again.

# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Arduino Uno Code
This is the code that I uploaded to my Arduino Uno, which was connected to the actual car.

```c++
#include <SoftwareSerial.h>

#define tx 2
#define rx 3



SoftwareSerial configBt(rx, tx);
long tm,t,d;

char c="";

const int TWOA1A = 4;
const int TWOA1B = 5;
//left side;
const int TWOB1A = 9;
const int TWOB1B = 8;
//right side;



void setup() {
  Serial.begin(38400);
  configBt.begin(38400);
  pinMode(tx, OUTPUT);
  pinMode(rx, INPUT);

  pinMode(TWOB1A,OUTPUT);
  pinMode(TWOB1B,OUTPUT);

  pinMode(TWOA1A,OUTPUT);
  pinMode(TWOA1B,OUTPUT);

}

void loop() {
  if(configBt.available()){
    c=(char)configBt.read();
    Serial.println(c);
  }

  switch(c){
    case 'f':
      forward();
      break;

    case 'b':
      back();
      break;

    case 'r':
      right();
      break;

    case 'l':
      left();
      break;

    case 's':
      stop();
      break;
  }
}


void forward(){
  digitalWrite(TWOA1A,LOW);
  digitalWrite(TWOA1B,HIGH);
  digitalWrite(TWOB1A,HIGH);
  digitalWrite(TWOB1B,LOW);
}

void back(){
  digitalWrite(TWOA1A,HIGH);
  digitalWrite(TWOA1B,LOW);
  digitalWrite(TWOB1A,LOW);
  digitalWrite(TWOB1B,HIGH);
}

void right(){
  digitalWrite(TWOA1A,HIGH);
  digitalWrite(TWOA1B,LOW);
  digitalWrite(TWOB1A,HIGH);
  digitalWrite(TWOB1B,LOW);
}

void left(){
  digitalWrite(TWOA1A,LOW);
  digitalWrite(TWOA1B,HIGH);
  digitalWrite(TWOB1A,LOW);
  digitalWrite(TWOB1B,HIGH);
}

void stop(){
  digitalWrite(TWOA1A,LOW);
  digitalWrite(TWOA1B,LOW);
  digitalWrite(TWOB1A,LOW);
  digitalWrite(TWOB1B,LOW);
}





```
# Arduino Micro Code
This was my code for the Arduino Micro which was connected to the controller of the car.
```c++
#include <Wire.h>

#define MPU6050_ADDRESS 0x68

int16_t accelerometerX, accelerometerY, accelerometerZ;

void setup()
{
  Wire.begin();
  Serial1.begin(38400);

  Wire.beginTransmission(MPU6050_ADDRESS);
  Wire.write(0x6B);
  Wire.write(0);
  Wire.endTransmission(true);
  delay(100);
}

void loop()
{
  readData();
  doMovement();
  delay(500);
}

void readData()
{
  Wire.beginTransmission(MPU6050_ADDRESS);
  Wire.write(0x3B);
  Wire.endTransmission(false);
  Wire.requestFrom(MPU6050_ADDRESS, 6, true); 

  accelerometerX = Wire.read() << 8 | Wire.read();
  accelerometerY = Wire.read() << 8 | Wire.read();
  accelerometerZ = Wire.read() << 8 | Wire.read();
}


void doMovement()
{
  if (accelerometerY >= 6500) {
    Serial1.write('f');
  }
  else if (accelerometerY <= -4000) {
    Serial1.write('b');
  }
  else if (accelerometerX <= -3250) {
    Serial1.write('l');
  }
  else if (accelerometerX >= 3250) {
    Serial1.write('r');
  }
  else {
    Serial1.write('s');
  }
}

```
# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Use** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Screwdriver Set | To tighten screw | $6.99 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6(https://www.amazon.com/Small-Screwdriver-Set-Mini-Magnetic/dp/B08RYXKJW9/)/"> Link </a> |
| H-Bridge | To control the motors | $5.99 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/(https://www.amazon.com/Ferwooh-Stepper-Controller-2-5-12V-H-Bridge/dp/B0D17PJ2MS/ref=sr_1_1?crid=2OQ7UJ1VJLUHU&dib=eyJ2IjoiMSJ9.xPgxMG6cmxZRuRbSqT3QxSr9zBhiCzp3WpnCeGbZjJfW2wU1eHonQ9Yw7yZi2k6Q3PhHd4uR1wLLWBETfHe0SF_wYRGvOug585fW0fsZTX6ImNTMLCJR3VH7MrRlnR7uQ5g0XrAXnzyVOSTEAmuNKyuiUk_vhsIuCNv1HCMrPUyPtn7qKFCwz7vVMcvEXx5Ddy4TPQJlpbS_voU9at8F85yJM5O9Hp5bbg_xuIHUsuE2ePCbv4lATgHmgHzENtlSRiU4laurwSqTAEgEnv9gNIbmb5d2HT5qBLfNChqSyio.9Fh1mUFHx48E8QZCOAX5T2ZJxzbHHdu93PJ63MLUqpM&dib_tag=se&keywords=L9110S+DC&s=electronics&sprefix=l9110s+dc%2Celectronics%2C89&sr=1-1)"> Link </a> |
| Arduino UNO | A microcontroller board used to control the car | $16.99 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/(https://www.amazon.com/ELEGOO-Board-ATmega328P-ATMEGA16U2-Compliant/dp/B01EWOE0UU/ref=sr_1_2_sspa?crid=3A6NCD2X9JEMJ&dib=eyJ2IjoiMSJ9.AcWZy-Yg4mDTnhzEHozxzPZdVC5-KUL2tW-OQewDKpBB4brSpD-p4bn74WcXiW3KarYertgpNaLJ0VHKx0qsPqolKAhiz1GRG5BwJQl73cEvrlXIXNmqlpSvU7uu2aRVSwAZi9Gj2AjSPLM3esW1Gzy9xEiQ9oiR5LCNjh4MlYDx5mTm5sI4rsD4CFTipJnF572qXlickl35FRcCj8oMXQotumgqI4yEIq0HobOtIlEnNhtVB51JMBHhqtmmF_PC9WeHJ4ySUVVcv_gq3_VeG1aAEbdm4NXmmT6NOYPw4Qo.1PFdgFT22oqO5Mg6-6j_aUL_EV8tUPuaFrB5N9oaEX0&dib_tag=se&keywords=elegoo+arduino&s=electronics&sprefix=elegoo+arduino%2Celectronics%2C99&sr=1-2-spons&sp_csd=d2lkZ2V0TmFtZT1zcF9hdGY&psc=1)"> Link </a> |
|8 piece DC Motor| These rotate the tires on the car | $10.99 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6(https://www.amazon.com/Small-Screwdriver-Set-Mini-Magnetic/dp/B08RYXKJW9/)/(https://www.amazon.com/AEDIKO-Motor-Gearbox-200RPM-Ratio/dp/B09N6NXP4H/ref=sr_1_4?crid=1JP29NIWBLH2M&dib=eyJ2IjoiMSJ9.Wq3jKgOLbqtEP772vMD4pV5f-w3PLBdEpKqguykXOb0JFO14f4Dq0m_VDVUMUFtR8WFINUEticI3GXcoGqwXPqK9yIh04PhCktgccMz9zAUiKXMJPwmOTUp_6av3XuFD0lXo9WngN9iKI6YgZrhEEs9qnqbcB1GnvgntCdKz8Q1dFuNu61NgSE6Z8vBk3FRpaNcr1lCI7FApTiNi0Qce8gbfmMn6oUggZQHpIOKKZ6s.M7WsZ_ZZtm3rm93kKgw0NOxt1McVBYX6m55oGxu1xxI&dib_tag=se&keywords=dc+motor+with+gearbox&sprefix=dc+motor+with+gearbox%2Caps%2C126&sr=8-4)"> Link </a> |
| Electronics Component Kit| Contains the wires and resistors I used | $13.99 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6(https://www.amazon.com/Small-Screwdriver-Set-Mini-Magnetic/dp/B08RYXKJW9/)/(https://www.amazon.com/Smraza-Electronics-Potentiometer-tie-Points-Breadboard/dp/B0B62RL725/ref=sxts_b2b_sx_reorder_acb_business?crid=2IC3T44H3U3WG&cv_ct_cx=breadboard+kit&dib=eyJ2IjoiMSJ9.TUd5tu2T8rmms7ZuJ0UzmbtpLL1zsu93bQM0PzwnP4E.sT0V0vL_QtbYv8ymVTCcRkhFNgBtRvRiT7G4FT1oGTE&dib_tag=se&keywords=breadboard+kit&sbo=RZvfv%2F%2FHxDF%2BO5021pAnSA%3D%3D&sprefix=breadboard+kit%2Caps%2C109&sr=1-2-9f062ed5-8905-4cb9-ad7c-6ce62808241a)"> Link </a> |
| 4PC Breadboard Kit | Made all the electronic connections and extended the h-bridge | $8.88 | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6(https://www.amazon.com/Small-Screwdriver-Set-Mini-Magnetic/dp/B08RYXKJW9/)/(https://www.amazon.com/Breadboards-Solderless-Breadboard-Distribution-Connecting/dp/B07DL13RZH/ref=sxts_b2b_sx_reorder_acb_business?crid=1RAL6PA1TZ81Q&cv_ct_cx=breadboard+kit&dib=eyJ2IjoiMSJ9.TUd5tu2T8rmms7ZuJ0UzmbtpLL1zsu93bQM0PzwnP4E.sT0V0vL_QtbYv8ymVTCcRkhFNgBtRvRiT7G4FT1oGTE&dib_tag=se&keywords=breadboard+kit&s=electronics&sbo=RZvfv%2F%2FHxDF%2BO5021pAnSA%3D%3D&sprefix=breadboard+kit%2Celectronics%2C102&sr=1-1-9f062ed5-8905-4cb9-ad7c-6ce62808241a)"> Link </a> |
|:--:|:--:|:--:|:--:|
# Resources that I used
These are some of the resources I used to help me build my car:
- [Gesture Controlled Robotic Arm by Joel A.]([https://trashytuber.github.io/YimingJiaBlueStamp/](https://jabraham777.github.io/Gesture_Controlled_Robotic_Car/))
- [Gesture Controlled Robot via Bluetooth]([https://sviatil0.github.io/Sviatoslav_BSE/](https://www.hackster.io/embeddedlab786/hand-gesture-control-robot-via-bluetooth-94b13d))
- [A document which helped me establish the Bluetooth connections]([https://arneshkumar.github.io/arneshbluestamp/](https://cdn.discordapp.com/attachments/1245042593717293137/1249801066216951919/Using_HC05_to_Communicate_to_HC05_1.docx?ex=66805a72&is=667f08f2&hm=fdc41341c4fdfdd7783f88b4ec2c15a814b22f760978444b4a3bb93779dd9a68&))

To watch the BSE tutorial on how to create a portfolio, click here.
