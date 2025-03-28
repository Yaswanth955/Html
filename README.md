#define BTN1 2  // Button for Lane 1 (simulating IR Sensor 1)
#define BTN2 3  // Button for Lane 2 (simulating IR Sensor 2)

#define RED1 4
#define YELLOW1 5
#define GREEN1 6

#define RED2 7
#define YELLOW2 8
#define GREEN2 9

void setup() {
    pinMode(BTN1, INPUT_PULLUP);
    pinMode(BTN2, INPUT_PULLUP);

    pinMode(RED1, OUTPUT);
    pinMode(YELLOW1, OUTPUT);
    pinMode(GREEN1, OUTPUT);

    pinMode(RED2, OUTPUT);
    pinMode(YELLOW2, OUTPUT);
    pinMode(GREEN2, OUTPUT);

    Serial.begin(9600);
}

void loop() {
    int lane1 = digitalRead(BTN1);
    int lane2 = digitalRead(BTN2);

    Serial.print("Lane 1: ");
    Serial.print(lane1);
    Serial.print(" | Lane 2: ");
    Serial.println(lane2);

    if (lane1 == LOW) {  // Vehicle detected in Lane 1
        digitalWrite(GREEN1, HIGH);  // Lane 1 Green ON
        digitalWrite(RED2, HIGH);    // Lane 2 Red ON
        delay(5000);  // Give full 5 seconds for green

        digitalWrite(GREEN1, LOW);
        digitalWrite(YELLOW1, HIGH);
        delay(2000);  // Yellow transition

        digitalWrite(YELLOW1, LOW);
        digitalWrite(RED1, HIGH);
        digitalWrite(GREEN2, HIGH);  // Lane 2 Green ON
        digitalWrite(RED2, LOW);
        delay(5000);  // Ensure full 5 seconds for green

        digitalWrite(GREEN2, LOW);
        digitalWrite(YELLOW2, HIGH);
        delay(2000);  // Yellow transition

        digitalWrite(YELLOW2, LOW);
        digitalWrite(RED2, HIGH);
        digitalWrite(RED1, LOW);
    } 
    else if (lane2 == LOW) {  // Vehicle detected in Lane 2
        digitalWrite(GREEN2, HIGH);  // Lane 2 Green ON
        digitalWrite(RED1, HIGH);    // Lane 1 Red ON
        delay(5000);  // Give full 5 seconds for green

        digitalWrite(GREEN2, LOW);
        digitalWrite(YELLOW2, HIGH);
        delay(2000);  // Yellow transition

        digitalWrite(YELLOW2, LOW);
        digitalWrite(RED2, HIGH);
        digitalWrite(GREEN1, HIGH);  // Lane 1 Green ON
        digitalWrite(RED1, LOW);
        delay(5000);  // Ensure full 5 seconds for green

        digitalWrite(GREEN1, LOW);
        digitalWrite(YELLOW1, HIGH);
        delay(2000);  // Yellow transition

        digitalWrite(YELLOW1, LOW);
        digitalWrite(RED1, HIGH);
        digitalWrite(RED2, LOW);
    } 
    else {  // No vehicle detected
        digitalWrite(RED1, HIGH);
        digitalWrite(RED2, HIGH);
        digitalWrite(GREEN1, LOW);
        digitalWrite(GREEN2, LOW);
        digitalWrite(YELLOW1, LOW);
        digitalWrite(YELLOW2, LOW);
    }

    delay(1000);
}
