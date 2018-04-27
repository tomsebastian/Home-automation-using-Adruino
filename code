#include <SoftwareSerial.h>
char tag[] ="11004E559A90"; // Replace with your own Tag ID
char input[12];        // A variable to store the Tag ID being presented
int count = 0;        // A counter variable to navigate through the input[] character array
boolean flag = 0;     // A variable to store the Tag match status
SoftwareSerial BT(10,11); // RX,TX
int Data;
#define LED1 8
#define LED2 9
#define LED3 12
#include <Servo.h>
Servo myservo;
void setup()
{
  Serial.begin(9600);   // Initialise Serial Communication with the Serial Monitor
  BT.begin(9600);
  BT.println("ACTIVE");
  pinMode(LED1,OUTPUT);
  pinMode(LED2,OUTPUT);
  pinMode(LED3,OUTPUT);
  myservo.attach(6);
}
void loop()
{
  if(Serial.available())// Check if there is incoming data in the RFID Reader Serial Buffer.
  {
    count = 0; // Reset the counter to zero
    /* Keep reading Byte by Byte from the Buffer till the RFID Reader Buffer is empty 
       or till 12 Bytes (the ID size of our Tag) is read */
    while(Serial.available() && count < 12) 
    {
      input[count] = Serial.read(); // Read 1 Byte of data and store it in the input[] variable
      count++; // increment counter
      delay(5);
    }
    /* When the counter reaches 12 (the size of the ID) we stop and compare each value 
        of the input[] to the corresponding stored value */
    if(count == 12) // 
    {
      count =0; // reset counter varibale to 0
      flag = 1;
      /* Iterate through each value and compare till either the 12 values are 
         all matching or till the first mistmatch occurs */
      while(count<12 && flag !=0)  
      {
        if(input[count]==tag[count])
        flag = 1; // everytime the values match, we set the flag variable to 1
        else
        flag= 0; 
                               /* if the ID values don't match, set flag variable to 0 and 
                                  stop comparing by exiting the while loop */
        count++; // increment i
      }
    }
    if(flag == 1) // If flag variable is 1, then it means the tags match
   {
      Serial.println("Access Allowed!");
      digitalWrite(LED1,HIGH);
      digitalWrite(LED2,HIGH);
      digitalWrite(LED3,HIGH);
      myservo.write(180);
      delay(5000);
      myservo.write(0);
      delay(5000); 
      }      
    else
    {
      Serial.println("Access Denied"); // Incorrect Tag Message
      
        BT.println("INTRUDER AT THE DOOR");
    }
    /* Fill the input variable array with a fixed value 'F' to overwrite 
    all values getting it empty for the next read cycle */
    for(count=0; count<12; count++) 
    {
      input[count]= 'F';
    }
    count = 0; // Reset counter variable
  }
  if (BT.available())
       {
   Data=BT.read();
   if(Data=='1')
   {   
   digitalWrite(LED1,HIGH);
   BT.println("LED1 ON");
   }
   if (Data=='2')
   {
   digitalWrite(LED1,LOW);
   BT.println("LED1 OFF");
   }
   if(Data=='3')
   {   
   digitalWrite(LED2,HIGH);
   BT.println("LED2 ON");
   }
   if (Data=='4')
   {
   digitalWrite(LED2,LOW);
   BT.println("LED2 OFF");
   }
   if (Data=='5')
   {
   digitalWrite(LED3,HIGH);
   BT.println("LED3 ON");
   }
   if (Data=='6')
   {
   digitalWrite(LED3,LOW);
   BT.println("LED3 OFF");
   }
   if (Data=='0')
   {
   digitalWrite(LED1,LOW);

   digitalWrite(LED2,LOW);

   digitalWrite(LED3,LOW);

   }
       }  
}
