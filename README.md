# [Ping Pong Game on Arduino R3](https://www.tinkercad.com/things/8B5LpJXjQRa)
Simulation of PING PONG Game on a 16x2 LCD Display using an Arduino Uno R3.
# Description & Key Design Points:
* This project is a 2-Player PING PONG Game on a 16x2 LCD Display and programmed to an Arduino Uno R3 using Arduino IDE.

## Semantics of the Game:
  * The Ball has a dimension of single LCD pixel.
  * The Paddles of Players are 3 LCD Pixel in height and single LCD Pixel Column in width.
  * The Middle position of the paddles is used as reference to move the paddles.
  *  Game Title appears as the simulation is started and the game starts when any one of the four Push-buttons is pressed.
  * Each player uses their respective "UP" and "DOWN" push-buttons to move their paddles.
  * A point is scored by the other Player each time the ball crosses the vertical Column path of the Paddle of the First Player.
  * Scores of both the players are displayed for 2 seconds each time a point is scored.
  * Ball and both the paddles are reset to initial positions after a point is scored by any player.
  * The First Player to achieve 10 points wins the game.
  * The Name of the Winner is Printed on Display for 5 seconds and the game resets.
## Hardware Setup:
  * 4 data lines are used to print to LCD Display.
  * Pins RS and E are respectively connected to digital pins 12 & 11.
  * Both GND & RW are connected to Ground. Vcc is connected to 5V.
  * VO is connected to the Output of potentiometer to adjust brightness of the LCD Display.
  * The pins D7, D6, D5 and D4 of the LCD Display are connected to digital pins 6, 7, 8 and 9 of the Arduino.
  * “UP” and “Down” push-buttons of Player 1 are connected to digital pins 5 and 10 respectively.
  * “UP” and “Down” push-buttons of Player 2 are connected to digital pins 2 and 3 respectively.

## Logic Behind the Ball:
  * The ball starts moving to the left(towards Player 1) when the game starts.
  * We use the X-Co-ordinate and Y-Co-ordinate to represent the location of the ball on the display.
  * We delete the previous location and light the next position of the ball.
  * We use the Horizontal(Xdir) and Vertical(YDir) direction parameters to calculate the next position
of the ball by adding the direction parameters to the Co-ordinates.
  * We invert the Vertical Direction parameter(YDir) of the ball if the ball reaches the top or bottom
pixel row of the screen.
  * We invert the Horizontal Direction parameter(XDir) of the ball if it hits the paddle of any player.
  * The Y-Direction parameter of the ball is set to (-1) if the ball hits the upper part of the paddle and
it’s set to (+1) if the ball hits the bottom part of the paddle and it’s left unchanged if the ball hits
the middle part of the paddle.
  * We invert both the X-Direction parameter and the Y-Direction parameter of the ball when the it
hits the paddle at the top(upper corner) or bottom(lower corner) of the display.
  * We increase the score of the other player if the ball reaches the pixel column behind the first
player’s paddle.
  * We reset the ball’s position and direction parameters each time a player scores.

## Miscellaneous
* To ensure that the speed of the ball remains almost same in every direction it travels i.e. both
horizontally and diagonally, the ball update time is kept at an approximate 1.414 times higher value
when moving diagonally than when it moves horizontally.
* The code is written using Object Oriented programming to take advantage of it's structural
properties.
* Any text to be printed on LCD Display is declared as F( ) Macro to save RAM as only 2048 bytes
are available.
* External Interrupts are employed to detect button press which made huge improvements on button
press detection over POLLING method.
* Port Manipulation allowed for faster digital reads and faster setting up of pin-modes.
* The “Up” and “down” button of Player 2 were assigned digital pins 2 & 3 becuase only digital pins
2 & 3 support External Interrupts
* “Up” Button of Player 1 was assigned digital Pin 5 of PORT D because different ports have separate
Pin Change Interrupt Routine for it’s pins. This move saved lines of code that would have been
required to identify the pin to which the interrupt belong.
* “Down” Button of Player 1 was assigned digital pin 10 of PORT B to facilitate ease of identifuing
PIN CHANGE INTERRUPT in the Interrupt Service Routine for PORT B.
