# ESP
This program measures distance using the HC-SR04 ultrasonic sensor with an ESP module. It sends an ultrasonic pulse, receives the echo, calculates the time taken, and computes the distance. The distance is displayed on the serial monitor every second.

## Code:
```
int t_p=5;
int e_p=18;
float ss=0.034;
long durn;
float dist_cm;


void setup() {
  
  Serial.begin(115200);
  pinMode(t_p, OUTPUT);
  pinMode(e_p, INPUT);
}

void loop() {
  
  digitalWrite(t_p, LOW);
  delayMicroseconds(2);
  digitalWrite(t_p, HIGH);
  delayMicroseconds(10);
  digitalWrite(t_p, LOW);
  durn=pulseIn(e_p,HIGH);
  dist_cm=durn*ss/2;
  Serial.print("distance= ");
   Serial.println(dist_cm);

  delay(1000); 
}
```
### How does this code work?
##### Let me explain each part of the code:

#### Variable Definitions:
```
int t_p = 5;
int e_p = 18;
float ss = 0.034;
long durn;
float dist_cm;
```
- `t_p`: Represents the pin number connected to the transmitter of the sensor.
- `e_p`: Represents the pin number connected to the receiver of the sensor.
- `ss`: Represents the speed of sound in meters per microsecond (approximately 0.034 cm/µs).
- `durn`: Variable to store the duration of the pulse from transmission to reception.
- `dist_cm`: Variable to store the calculated distance.

#### `setup` Function:
```
void setup() {
  Serial.begin(115200);
  pinMode(t_p, OUTPUT);
  pinMode(e_p, INPUT);
}
```
- `Serial.begin(115200)`: Initializes serial communication at a baud rate of 115200.
- `pinMode(t_p, OUTPUT)`: Sets the transmitter pin as an output.
- `pinMode(e_p, INPUT)`: Sets the receiver pin as an input.

#### `loop` Function:
```
void loop() {
  digitalWrite(t_p, LOW);
  delayMicroseconds(2);
  digitalWrite(t_p, HIGH);
  delayMicroseconds(10);
  digitalWrite(t_p, LOW);
  durn = pulseIn(e_p, HIGH);
  dist_cm = durn * ss / 2;
  Serial.print("distance= ");
  Serial.println(dist_cm);
  delay(1000); 
}
```
- `digitalWrite(t_p, LOW)`: Ensures the transmitter pin is low (0 volts) to start the signal.
- `delayMicroseconds(2)`: Waits for 2 microseconds.
- `digitalWrite(t_p, HIGH)`: Sends a high pulse (5 volts) for 10 microseconds.
- `delayMicroseconds(10)`: Waits for 10 microseconds.
- `digitalWrite(t_p, LOW)`: Sets the transmitter pin back to low.
- `durn = pulseIn(e_p, HIGH)`: Measures the time taken for the echo pulse to return using pulseIn.
- `dist_cm = durn * ss / 2`: Calculates the distance based on the time taken and the speed of sound, divided by 2 because the signal travels to the object and back.
- `Serial.print("distance= ") and Serial.println(dist_cm)`: Prints the calculated distance to the serial monitor.
- `delay(1000)`: Waits for one second before repeating the process.

![i1](https://github.com/user-attachments/assets/d06c61f0-d52b-42b7-b3a7-66d194a1370c)


### How the HC-SR04 Sensor Works:
1. The sensor sends an ultrasonic pulse via the transmitter.
2. The pulse reflects off an object and returns to the receiver.
3. The time between sending and receiving the pulse is measured.
4. Using the speed of sound, the distance between the sensor and the reflecting object can be calculated.

## Summary:
The program repeatedly sends ultrasonic pulses, measures the time taken for the echo to return, calculates the distance to the object, and displays this distance on the serial monitor every second. This allows you to see the real-time distance measurement between the sensor and the object.
