#include <Servo.h>
float z,temp;
int outputValue = 0;
int ultrsValue = 0;
int pirValue = 0;
int const LDR = A5;
int const gas_sensor = A1;
int limit = 300;



long readUltrasonicDistance(int triggerPin, int echoPin)
{
  pinMode(triggerPin, OUTPUT);  // Clear the trigger
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);
// Sets the trigger pin to HIGH state for 10 microseconds
  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW);
  pinMode(echoPin, INPUT);
  // Reads the echo pin, and returns the sound wave travel time in microseconds
  return pulseIn(echoPin, HIGH);
}

Servo doorlock;

void setup()
{
  Serial.begin(9600);		//initialize serial communication
  pinMode(A5, INPUT);		//LDR
  pinMode(A1,INPUT);      	//gas sensor
  pinMode(12, OUTPUT);		//connected to relay
  doorlock.attach(7, 500, 2500); //servo motor
  pinMode(A4, INPUT);
  pinMode(8,OUTPUT);     	//signal to piezo buzzer
  pinMode(10, INPUT);		//signal to PIR	
  pinMode(11, OUTPUT);		//signal to npn as switch
}

void loop()
{
  
  //--------------------------------------------------------------  
        //------ light control --------// 
//--------------------------------------------------------------
     
  
  int val1 = analogRead(LDR);

  if (val1 > 500) 
  	{
    	digitalWrite(12, LOW);
    Serial.print("Bulb ON = ");
    Serial.print(val1);
  	} 
  else 
  	{
    	digitalWrite(12, HIGH);
     Serial.print("Bulb OFF = ");
    Serial.print(val1);
  	}

//--------------------------------------------------------------  
        //------ fan control --------// 
//--------------------------------------------------------------
 
  
  
 
  z= analogRead(A4);
  Serial.println(z);
  temp = (double)z / 1024;   //find percentage of input reading
  temp = temp * 5;                     //multiply by 5V to get voltage
  temp = temp - 0.5;                   //Subtract the offset 
  temp = temp * 100;                   //Convert to degrees 
  pirValue = digitalRead(10);
 
  
  if ( (pirValue == 1) )
  {
  
   if  (temp>30)
    {
      digitalWrite(11, HIGH);
   }
  else if (temp<30)
  {
  digitalWrite(11, LOW);  
  }
    else
   {
    digitalWrite(11, LOW); //npn as switch OFF
    Serial.print("     || NO Motion Detected    " );
   }
  }
  
  	
 
  
  
       // ------- Gas Sensor --------//
  
   
  int val = analogRead(gas_sensor);      //read sensor value
  Serial.print(" GAS ");
  Serial.print(val);				   //Printing in serial monitor

  if (val > limit)
  	{
    	tone(8, 650);
  	}
 	delay(300);
 	noTone(8);
  
      //-------  servo motor  ---------//
  
  ultrsValue = 0.01723 * readUltrasonicDistance(6, 6);

  if (ultrsValue < 100) 
  	{
    	doorlock.write(90);
    Serial.print(" ");
    Serial.print(ultrsValue);
   Serial.print("\n");
 
  	} 
  else 
  	{
    	doorlock.write(0);
    Serial.print("  ");
    Serial.print(ultrsValue);
    Serial.print("\n");
  }
  delay(10); // Delay a little bit to improve simulation performance
}
