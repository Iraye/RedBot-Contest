//Sensortest_2
#include <RedBot.h>
#include <MsTimer2.h>

// H-Bridge motor driver pins
#define    L_CTRL1   2
#define    L_CTRL2   4
#define    L_PWM     5

#define    R_CTRL1   7
#define    R_CTRL2   8
#define    R_PWM     6

// XBee SW_Serial pins
#define    SW_SER_TX A0
#define    SW_SER_RX A1

RedBotSensor lSen = RedBotSensor(A1);
RedBotSensor mSen = RedBotSensor(A2);
RedBotSensor rSen = RedBotSensor(A3);

long i;

/*******************
/ setup function
/*******************/
void setup()
{
    Serial.begin(9600);

    pinMode(L_CTRL1, OUTPUT);  // used as a debug pin for an LED.
    pinMode(L_CTRL2, OUTPUT);  // used as a debug pin for an LED.
    pinMode(L_PWM, OUTPUT);  // used as a debug pin for an LED.

    pinMode(R_CTRL1, OUTPUT);  // used as a debug pin for an LED.
    pinMode(R_CTRL2, OUTPUT);  // used as a debug pin for an LED.
    pinMode(R_PWM, OUTPUT);  // used as a debug pin for an LED.

    pinMode(13, OUTPUT);  // used as a debug pin for an LED.
    
    i = 0;
}

/*******************
/ loop function
/*******************/
void loop()
{
    
    //leftMotor(-60);
    //rightMotor(-60);
    Serial.println("\nReading number: ");
    Serial.println(i);
    Serial.println("\nLeft sensor:\n");
    Serial.println(lSen.read());
    Serial.println("\nMid sensor:\n");
    Serial.println(mSen.read());
    Serial.println("\nRigth sensor:\n");
    Serial.println(rSen.read());
    i++;
    delay(200);
    
}

/*******************************************************************************/
void leftMotor(int motorPower)
{
    motorPower = constrain(motorPower, -255, 255);   // constrain motorPower to -255 to +255
    if(motorPower >= 0)
    {
        // spin CW
        digitalWrite(L_CTRL1, HIGH);
        digitalWrite(L_CTRL2, LOW);
        analogWrite(L_PWM, abs(motorPower));
    }
    else
    {
        // spin CCW
        digitalWrite(L_CTRL1, LOW);
        digitalWrite(L_CTRL2, HIGH);
        analogWrite(L_PWM, abs(motorPower));
    }
}

/*******************************************************************************/
void rightMotor(int motorPower)
{
    motorPower = constrain(motorPower, -255, 255);   // constrain motorPower to -255 to +255
    if(motorPower >= 0)
    {
        // spin CW
        digitalWrite(R_CTRL1, HIGH);
        digitalWrite(R_CTRL2, LOW);
        analogWrite(R_PWM, abs(motorPower));
    }
    else
    {
        // spin CCW
        digitalWrite(R_CTRL1, LOW);
        digitalWrite(R_CTRL2, HIGH);
        analogWrite(R_PWM, abs(motorPower));
    }
}

