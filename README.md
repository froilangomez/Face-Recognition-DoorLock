# Face-Recognition-DoorLock
#include <Wire.h>
#include "HUSKYLENS.h"

HUSKYLENS huskylens;

// Define the solenoid pin
const int solenoidPin = 7;

void setup() {
    Serial.begin(9600);
    Wire.begin();
    huskylens.begin(Wire);
    pinMode(solenoidPin, OUTPUT);
    digitalWrite(solenoidPin, LOW); // Ensure solenoid is locked initially
}

void loop() {
    if (huskylens.request()) { // Request data from HuskyLens
        if (huskylens.isLearned() && huskylens.readBlock(0)) { // Check if a learned face is detected
            if (huskylens.id == YOUR_FACE_ID) { // Replace YOUR_FACE_ID with the actual ID of your face
                digitalWrite(solenoidPin, HIGH); // Unlock the solenoid
                delay(5000); // Keep unlocked for 5 seconds
                digitalWrite(solenoidPin, LOW); // Lock again
            }
        }
    }
}
huskylens.id
