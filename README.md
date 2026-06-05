# micro-mouse-code

int motor1pin1 = 2;
int motor1pin2 = 3;

int motor2pin1 = 4;
int motor2pin2 = 5;
const int trigPinF = 12;
const int echoPinF = 11;
const int trigPinR = 6;
const int echoPinR = 7;
const int trigPinL = 13;
const int echoPinL = 8;
float durationF;
float durationL;
float durationR;
float distanceF;
float distanceL;
float distanceR;
//Pin 10 controls right motor speed
//Pin 9 controls left motor speed


void setup() {
  // put your setup code here, to run once:
  
pinMode(motor1pin1, OUTPUT);
 pinMode(motor1pin2, OUTPUT);
 pinMode(motor2pin1, OUTPUT);
 pinMode(motor2pin2, OUTPUT);
 pinMode(9, OUTPUT);
 pinMode(10, OUTPUT);
 pinMode(trigPinF, OUTPUT);
 pinMode(echoPinF, INPUT);
 pinMode(trigPinR, OUTPUT);
 pinMode(echoPinR, INPUT);
 pinMode(trigPinL, OUTPUT);
 pinMode(echoPinL, INPUT);
 Serial.begin(9600);
}
void loop() {
  Serial.print("DistanceF: ");
  Serial.println(distanceF);  
 digitalWrite(trigPinF, LOW);
 delayMicroseconds(2);
 digitalWrite(trigPinF, HIGH);
 delayMicroseconds(10);
 digitalWrite(trigPinF, LOW);

 durationF = pulseIn(echoPinF, HIGH, 30000);
 distanceF = (durationF*.034)/2;

 digitalWrite(trigPinR, LOW);
 delayMicroseconds(2);
 digitalWrite(trigPinR, HIGH);
 delayMicroseconds(10);
 digitalWrite(trigPinR, LOW);

durationR = pulseIn(echoPinR, HIGH, 30000);
 distanceR = (durationR*.034)/2;

 digitalWrite(trigPinL, LOW);
 delayMicroseconds(2);
 digitalWrite(trigPinL, HIGH);
 delayMicroseconds(10);
 digitalWrite(trigPinL, LOW);

 durationL = pulseIn(echoPinL, HIGH, 30000);
 distanceL = (durationL*.034)/2;

 Serial.print(" F: ");
Serial.print(distanceF);

Serial.print(" R: ");
Serial.print(distanceR);

Serial.print(" L: ");
Serial.println(distanceL);

 

 
 if (distanceF <= 6.25 and distanceR < distanceL) {
  analogWrite(9, 74);
  analogWrite(10, 88);
  digitalWrite(motor1pin1, LOW);
  digitalWrite(motor1pin2, HIGH);
  digitalWrite(motor2pin1, HIGH);
  digitalWrite(motor2pin2, LOW);
 }
 else if (distanceF <= 6 and distanceL <= distanceR) {
  analogWrite(9, 79);
  analogWrite(10, 55);
  digitalWrite(motor1pin1, HIGH);
  digitalWrite(motor1pin2, LOW);
  digitalWrite(motor2pin1, LOW);
  digitalWrite(motor2pin2, HIGH);
 }
 else{
  analogWrite(9, 58);
  analogWrite(10, 47);
    if (distanceL < 6){
  digitalWrite(motor1pin1, HIGH);
  digitalWrite(motor1pin2, LOW);
  digitalWrite(motor2pin1, LOW);
  digitalWrite(motor2pin2, HIGH);
  }
  else if (distanceR < 6){
  digitalWrite(motor1pin1, LOW);
  digitalWrite(motor1pin2, HIGH);
  digitalWrite(motor2pin1, HIGH);
  digitalWrite(motor2pin2, LOW);
  }
  else{
  digitalWrite(motor1pin1, HIGH); 
  digitalWrite(motor1pin2, LOW);
  digitalWrite(motor2pin1, HIGH);
  digitalWrite(motor2pin2, LOW);
  }
 }
}
