Documentação do Código

# **__Binary Adder__**

Institution
Technical in Systems Development - SENAC NH

Student:
Rafael Matielli

Professor:
Glauber Kiss de Souza

Subject:
Technical Analysis and Orientation

General Description

This program is developed for an Arduino microcontroller. It performs the addition of two 4-bit numbers, read from digital input pins, and displays the result on digital output pins, including the carry bit.

Global Variables

soma: Variable to store the value read from pin 13, indicating whether the addition should be performed.

carryBit: Stores the carry bit during addition.

nib1a, nib1b, nib1c, nib1d: Bits of the first 4-bit number.

nib2a, nib2b, nib2c, nib2d: Bits of the second 4-bit number.

res1a, res1b, res1c, res1d: Results of the addition for each bit.

Functions

void setup()

Configures digital pin modes:

Pins 0 to 7 are configured as inputs to read the bits of the numbers to be added.

Pins 8 to 12 are configured as outputs to display the addition result.

Pin 13 is configured as an input to read the flag that activates the addition.

cpp
Copiar código
void setup()
{
    pinMode(0, INPUT);
    pinMode(1, INPUT);
    pinMode(2, INPUT);
    pinMode(3, INPUT);
    pinMode(4, INPUT);
    pinMode(5, INPUT);
    pinMode(6, INPUT);
    pinMode(7, INPUT);
    pinMode(8, OUTPUT);
    pinMode(9, OUTPUT);
    pinMode(10, OUTPUT);
    pinMode(11, OUTPUT);
    pinMode(12, OUTPUT);
    pinMode(13, INPUT);
}
int somaBit(int b1a, int b2a, int cBit)

Performs addition of two bits (b1a and b2a) and a carry bit (cBit). Returns the result bit (without the carry).

cpp
Copiar código
int somaBit(int b1a, int b2a, int cBit)
{
    int bitResult = 0;
    
    if ((b1a ^ b2a) ^ cBit)
    {
        bitResult = 1;
    }
    else
    {
        bitResult = 0;
    }
    
    return bitResult;
}
int somaCarryBit(int b1a, int b2a, int cBit)

Calculates the carry bit resulting from the addition of two bits (b1a and b2a) and a carry bit (cBit). Returns the carry bit.

cpp
Copiar código
int somaCarryBit(int b1a, int b2a, int cBit)
{
    if ((b1a && b2a) || (b1a && cBit) || (b2a && cBit))
    {
        cBit = 1;
    }
    else
    {
        cBit = 0;
    }
    
    return cBit;
}
Execution Flow

Continuously executes the following steps:

Reads the addition flag from pin 13.
Reads the bits of the two numbers from pins 0 to 7.
If the addition flag is active (soma == 1), performs bit-by-bit addition of the two numbers, considering the carry.
Writes the addition results and the carry bit to pins 8 to 12.
cpp
Copiar código
void loop()
{
    soma = digitalRead(13);
    nib1a = digitalRead(0);
    nib1b = digitalRead(1);
    nib1c = digitalRead(2);
    nib1d = digitalRead(3);
    nib2a = digitalRead(4);
    nib2b = digitalRead(5);
    nib2c = digitalRead(6);
    nib2d = digitalRead(7);
    
    if (soma == 1)
    {
        carryBit = 0;
        res1a = somaBit(nib1a, nib2a, carryBit);
        carryBit = somaCarryBit(nib1a, nib2a, carryBit);
        res1b = somaBit(nib1b, nib2b, carryBit);
        carryBit = somaCarryBit(nib1b, nib2b, carryBit);
        res1c = somaBit(nib1c, nib2c, carryBit);
        carryBit = somaCarryBit(nib1c, nib2c, carryBit);
        res1d = somaBit(nib1d, nib2d, carryBit);
        carryBit = somaCarryBit(nib1d, nib2d, carryBit);
    }
    
    digitalWrite(8, res1a);
    digitalWrite(9, res1b);
    digitalWrite(10, res1c);
    digitalWrite(11, res1d);
    digitalWrite(12, carryBit);
}
Program Installation

Materials Required

Arduino Board (any model compatible with digital pins).
USB cable to connect Arduino to the computer.
Arduino IDE software installed on the computer.
Breadboard and connecting wires.
Buttons or switches to simulate digital inputs (optional).
Installation Steps

Hardware Setup

Connect input wires to Arduino pins 0 to 7.
Connect output wires to Arduino pins 8 to 12.
Connect a button or switch to pin 13 to activate the addition.
Software Setup

Open Arduino IDE on the computer.
Connect the Arduino board to the computer using the USB cable.
Select the Arduino board and correct port from the "Tools" menu.
Uploading the Code

Copy the provided code to the text editor in Arduino IDE.

Click on "Verify" to compile the code and check for errors.

Click on "Load" to send the compiled code to the Arduino board.

Commands to Run the Program

Compiling and Uploading the Code

Open Arduino IDE.
Paste the code into the editor.
Click on the "Verify" button (check icon) to compile.
Click on the "Load" button (arrow icon) to upload the code to Arduino.
Program Operation

After the code is uploaded, Arduino will start running automatically.
Set the input pins to the bits of the numbers you want to add.
Activate the button/switch connected to pin 13 to perform the addition.
Observe the output pins (8 to 12) to see the addition result.
Summary

This Arduino program reads two 4-bit numbers from input pins, performs bit-by-bit addition considering the carry bit, and displays the result on output pins. Installation is straightforward, involving digital pin configuration and code uploading via Arduino IDE.







