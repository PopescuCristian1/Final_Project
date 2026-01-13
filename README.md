# Smart Safe

## General Description
For my final project, I decided to build a security system that mimics the feel of an old-school mechanical safe, but with a digital brain. Instead of using a boring numeric keypad (which is what everyone does), I wanted to use a potentiometer to create a "rotary dial" interface. You turn the knob to find the numbers, and the system gives you visual feedback on an LCD and physical feedback via a servo motor lock.

## Features 
Analog "Rotary Dial" Interface: Simulates a mechanical safe dial using a potentiometer, converting analog rotation into precise digital selection.
Intelligent Signal Processing: Uses a custom "window of tolerance" algorithm to stabilize noisy sensor inputs for a smooth user experience.
Security Logic: Features a penalty lockout system (time-out) after failed attempts and persistent password storage using EEPROM (memory works even after power loss).
State Machine Architecture: The system relies on a robust Finite State Machine (Idle, Parsing, Validation, Lockout) rather than simple linear code.

## Bill of Materials
- Arduino Uno
- LCD 
- 10kΩ Potentiometer 
- Push Button (Select/Enter)
- SG90 Micro Servo (The Lock)
- Active Buzzer
- 9V Battery or USB Cable
- Breadboard, Wires, 1x 10kΩ Resistor

Aprox. 100 lei.

## Tutorial
I m not following a specific tutorial.

## Q1: What is the system boundary ?
Inside the system: The Arduino Uno, the LCD, the inputs (knob/button), and the actuator (servo). 
Basically, everything that sits on my desk. Outside the system: Me (the user), the power source, and the physical box I'm attaching this to. 
Definition: I define the boundary at the physical interface. The system starts processing the moment I touch the dial, and it ends when the servo arm physically moves the latch. It’s a standalone device.

## Q2:Where does the intelligence live ?
The "brains" of the operation are in the Finite State Machine (FSM) I'm writing for the Arduino. I'm not just writing a linear script; I'm coding distinct states:
1. Idle: Waiting for me to touch it.
2. Parsing: translating my knob rotation into numbers.
3. Validation: Checking my input against the saved password.
4. Lockout: A "penalty box" state that refuses input if I get the code wrong 3 times.

## Q3: What is the hardest tehnical problem ?
I think the biggest headache will be Signal Stability. Potentiometers are imperfect analog devices. If I turn the knob to a spot between "4" and "5", the electrical noise might make the screen flicker rapidly between the two numbers. My plan: I need to implement a "window of tolerance" in the code. I only want the number to change if I deliberately turn the knob past a certain threshold, ensuring the UI feels smooth and not glitchy.

## Q4: What is the minimum demo ?
At a minimum, I want to show:
1. The system powering up in a "Locked" state.
2. Me turning the knob and seeing clean, stable numbers 0-9 on the LCD.
3. Entering the correct code and seeing the Servo move 90 degrees to "Open."
4. Entering a wrong code and hearing the error buzzer.

## Q5: Why is this not just a tutorial ?
A tutorial usually teaches you how to wire a component and run a generic example. I am building a product prototype.
I m adding data persistence (EEPROM).
I m solving a UX problem (making an analog knob feel digital and precise), which requires much more complex math than just reading a button press.
I m implementing non-blocking timers for the security lockout, so the system doesn't just freeze up completely but stays responsive.

### I don t need an ESP32.
