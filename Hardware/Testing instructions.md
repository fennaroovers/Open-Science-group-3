**Instruction for testing the gearbox**

1) Put a rubbery adaptor on the cylinder that is exiting on the top part (this is an example, but other options may work). Place the gearbox on the black box. Then clip the black box onto the table to fix it. Place it near the spinning wheel.

![image 1](https://github.com/fennaroovers/Open-Science-group-3/blob/main/Images%20testing/Image%201.png)

2) Connect the power source wires to the motor.

![image 2](https://github.com/fennaroovers/Open-Science-group-3/blob/main/Images%20testing/Image%202.png)

3) Move the spinning wheel so that it is in contact with the rubbery adaptor.

![image 3](https://github.com/fennaroovers/Open-Science-group-3/blob/main/Images%20testing/Image%203.png)

4) The arduino circuit that should be on the desk has a sensor, fix it to the table, bellow the magnets of the wheel

![image 4](https://github.com/fennaroovers/Open-Science-group-3/blob/main/Images%20testing/Image%204.png)

5) Download the Arduino IDL software, open it and compile this code to the board. This code will show in the serial monitor the rpm at which the wheel is spinning.

int quarter_revolutions;

int ledPin = 12;

unsigned int rpm;

unsigned long timeold;

unsigned long now;



void setup() {

 Serial.begin(9600);
 
 attachInterrupt(0, magnet_detect, RISING);
 
 quarter_revolutions = 0;
 
 rpm = 0;
 
 timeold = 0;
 
 pinMode(ledPin, OUTPUT);
 
}


void loop() {

 if (quarter_revolutions >= 10) {

   now = millis();
   
   rpm = (quarter_revolutions * 60000.0) / ((now - timeold) * 4);
   
   timeold = now;
   
   quarter_revolutions = 0;
   
   Serial.print("RPM: ");
   
   Serial.println(rpm,DEC);
   
 }
}


void magnet_detect() {

 unsigned long now = millis();
 
 quarter_revolutions++;
 
 Serial.print("Signal detected at timestamp: ");
 
 Serial.print(now);
 
 Serial.println("ms");
}


6) Now to make the wheel spin at a certain velocity we tune the values of voltage and current.
   - For 8 RPM, we had to put in 1V, 0.5A - play around with similar values.

![image 5](https://github.com/fennaroovers/Open-Science-group-3/blob/main/Images%20testing/Image%205.png)

   - Your computer should show something like this:

![image 6](https://github.com/fennaroovers/Open-Science-group-3/blob/main/Images%20testing/Image%206.png)

   - For 8 RPM, we had to put in 3V, 0.8A - play around with similar values.

![image 7](https://github.com/fennaroovers/Open-Science-group-3/blob/main/Images%20testing/Image%207.png)

