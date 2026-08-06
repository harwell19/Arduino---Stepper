# Arduino---Stepper
## With this code, you'll have the basic tool to spinning a stepper motor. It start from 0 to 150 RPM, it is an abrupt acceleration, real stepper motors do not operate in that way. 

/*Running infinitely a stepper shaft at 150RPM*/

#define dirPin 2
#define stepPin 3
int stepsPerRev = 200;
int rpm = 150;
unsigned long stepInterval;
unsigned long lastStepMicros = 0;
int stepState = LOW;

void setup(){
  Serial.begin(115200);
  pinMode(dirPin, OUTPUT);
  pinMode(stepPin, OUTPUT);
  stepInterval = 60000000UL / (rpm * stepsPerRev * 2.);
  digitalWrite(dirPin, HIGH);
}

void loop(){
  unsigned long currentStepMicros = micros();
  if(currentStepMicros - lastStepMicros >= stepInterval){
    lastStepMicros += stepInterval;
    stepState = (stepState == LOW)? HIGH:LOW;
    digitalWrite(stepPin, stepState);

    unsigned long currentSpeed = 60000000UL / (stepsPerRev * stepInterval *2.);
    Serial.print("RPM: ");
    Serial.println(currentSpeed);
  }
}
