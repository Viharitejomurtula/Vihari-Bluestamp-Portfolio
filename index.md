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

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

-The first step towards this modification was to build the actual robotic arm itself. This was quite simple as I just followed a tutorial.
-The next step was to change the controls of the robotic arm, from the joysticks to the accelerometer. So I had to pair another two bluetooths that would make the Arduino Micro and the Nano board communicate. This was an issue as this meant I had to connect two bluetooth devices to the Arduino Micro. Initially I didn't think this was possible as the bluetooth just wouldn't connect to the Serial Port which was used to send messages. I fixed this problem by configuring the bluetooth while connecting it to the Nano and then just transferring the wiring over
-This was where I am at this point, but I hope to be able to alter the code uploaded into the arm to change the input of the if conditions from a joystick movement to an accelerometer reading



# Second Milestone

**After getting the controller working, I had to get the actual tires of the car rotating how I wanted them to.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/y3VAmNlER5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

-The first thing I did was understand the workings of the h-bridge, and used two of them to control the right two and left two wheels. This was an issue as I needed the left two tires to move in synch with each other as well as the right two tires to move in synch with each other.
-By extending the connections of the h-bridge to a breadboard, I was able to synch up the right two and left two wheels. 
-I faced an issue after doing this, there wasn't enough power to rotate all the motors. I fixed this by plugging a 9V battery into the Arduino UNO
-Finally, I connected an accelerometer to the Arduino Micro, which is the controller of the car. An accelerometer is able to sense the tilt in itself and manifest that tilt as a number in the x or y direction. Then I programmed the Micro to be able to send over the readings on the accelerometer to the car. This made it so that the car would move in accordance to the tilt of the controller.

# First Milestone

**Getting the Bluetooths on the car and the controller to be synched was a challenging task for me who has never dealt with this kind of a project before. But eventually, I got it to work and completed the first step of this project.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/CaCazFBhYKs" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

-The first step was to set up the wiring according to the wiring diagram. I kept messing this up because I kept confusing different wires and didn't understand how the breadboard worked, but eventually I got it wired properly.
-The next step was to understand what the code was actually doing. This wasn't too difficult as I just looked up all the syntax in the Arduino language references
-Finally, I had to configure the two bluetooths into a master and slave configuration. This took quite long as I kept messing up the AT commands which were involved with configuring the bluetooths, but I was successful after resetting the firmware and entering the commands again.

# Schematics 
Here's where you'll put images of your schematics. [Tinkercad](https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. 

# Code
Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. 

```c++
void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  Serial.println("Hello World!");
}

void loop() {
  // put your main code here, to run repeatedly:

}
```

# Bill of Materials
Here's where you'll list the parts in your project. To add more rows, just copy and paste the example rows below.
Don't forget to place the link of where to buy each component inside the quotation marks in the corresponding row after href =. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize this to your project needs. 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |
| Item Name | What the item is used for | $Price | <a href="https://www.amazon.com/Arduino-A000066-ARDUINO-UNO-R3/dp/B008GRTSV6/"> Link </a> |

# Other Resources/Examples
One of the best parts about Github is that you can view how other people set up their own work. Here are some past BSE portfolios that are awesome examples. You can view how they set up their portfolio, and you can view their index.md files to understand how they implemented different portfolio components.
- [Example 1](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Example 2](https://sviatil0.github.io/Sviatoslav_BSE/)
- [Example 3](https://arneshkumar.github.io/arneshbluestamp/)

To watch the BSE tutorial on how to create a portfolio, click here.
