const int servoPin = 9;     // Pin which the servo is attached to
const int servoRunTime = 1000; // How many milliseconds the servo got to move before getting disabled
#define TWEAK 10

int angles[] = {
  0,
  5 - TWEAK,
  15 - TWEAK,
  30 - TWEAK,
  45 - TWEAK,
  70 - TWEAK,
  85 - TWEAK,
  105 - TWEAK,
  130 - TWEAK,
  145 - TWEAK,
  160 - TWEAK,
  175
};

unsigned long servoTime = 0; // Store when the servo was activated

unsigned int feederPosition = 0;

unsigned long feedLast = 0;

#include <Servo.h>
Servo myservo;

void setup()
{
  setServo(angles[feederPosition]); // Move servo to first position in angles[]
}

void loop()
{
  if (millis() - feedLast >= 86400000UL) // 86400000 = 1 day in milliseconds
  {
    feedLast = millis(); // Store when this function is being run    
    feederPosition++; // Increase the position we want to move to
    setServo(angles[feederPosition]); // Command servo to move
  }
  
  handleServo(); // Continuously monitor if we need to detach the servo again
}

void setServo(int pos)
{
  if (servoTime == 0) // If servoTime is zero, we need to attach the servo before controlling it
  {
    myservo.attach(servoPin); // Attaching the servo to the servoPin
  }
  myservo.write(pos); // Send the position to the servo
  servoTime = millis(); // Store the time for when we send the position
}

void handleServo()
{
  if (servoTime != 0 && millis() - servoTime >= servoRunTime) // if servoTime isnt zero, and if more milliseconds has passed than defined by servoRunTime
  {
    servoTime = 0; // Set servoTime to zero, so we wont do this again until needed
    myservo.detach(); // Detach the servo so it wont destroy itself
  }
}
