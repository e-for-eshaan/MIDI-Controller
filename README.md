# MIDI-Controller

## Introduction:

A MIDI controller is a device used in music production and performance to generate and control MIDI data. It provides a hands-on interface with keys, pads, buttons, knobs, and sliders, allowing musicians to interact with MIDI-compatible software and hardware devices. MIDI controllers enable real-time control of virtual instruments, parameter adjustments, and recording MIDI data, enhancing the creative process in electronic music production.

![midi](https://github.com/e-for-eshaan/MIDI-Controller/assets/76566992/09b1b0ab-9fc0-4909-889a-b8d266ea7fc0)

## readPots.ino:

This file contains the readPots() function, which reads the values from five potentiometers (pot1, pot2, pot3, pot4, pot5) using the analogRead() function. It then calculates the difference between the new value and the last recorded value for each potentiometer. If the difference exceeds a certain threshold (diff), it sends a MIDI message using the MIDImessage() function.

![pots](https://github.com/e-for-eshaan/MIDI-Controller/assets/76566992/1922439c-8110-4101-bcf4-d1961104b86b)

The MIDI message is sent with the status byte 177, which represents a Control Change message. The second byte represents the control number (0-4 for the five potentiometers), and the third byte is the mapped value of the potentiometer reading in the range of 0-127.

## readKeyPad.ino:

This file contains the readKeyPad() function, which reads input from a keypad using the Keypad library. The keypad is scanned to detect keys that have changed their state (pressed or released). When a key is pressed, a MIDI "Note On" message is sent using the MIDImessage() function, and when a key is released, a MIDI "Note Off" message is sent.

![keypad](https://github.com/e-for-eshaan/MIDI-Controller/assets/76566992/f034bf99-a448-4afa-a7cc-5bf2a781631e)


The MIDI messages are sent with the status byte 144 (channel 1 Note On) for the "Note On" messages and 128 (channel 1 Note Off) for the "Note Off" messages. The second byte represents the note number, which is calculated based on the key pressed and the transpose value. The third byte is the velocity (127 for "Note On" and 0 for "Note Off").

The transpose value can be adjusted using two toggle switches (transposePin1 and transposePin2) to shift the keypad mapping up or down the scale by one octave.

## readJoystick.ino:

This file contains the readJoystick() function, which reads input from a joystick. It reads the values of the X-axis and Y-axis potentiometers of the joystick using the analogRead() function. The X-axis reading is sent as a MIDI Control Change message, while the Y-axis reading is sent as a modulation MIDI message.

The X-axis MIDI message is sent with the status byte 176, representing a Control Change message on channel 1. The second byte represents the control number (1), and the third byte is the mapped value of the joystick X-axis reading in the range of 127-0.

The Y-axis modulation MIDI message is sent with the status byte 224, representing a Pitch Bend message. The third byte of the message is constructed using the joystick Y-axis reading, mapping it to a 14-bit value (-8000 to 8000) and splitting it into two 7-bit values.

The joystick readings are only sent if the corresponding toggle switch (Xswitch for X-axis, Yswitch for Y-axis) is in the correct position.

## MIDImessage.ino:

This file contains the MIDImessage() function, which takes three arguments: the status byte, and two data bytes. It sends the MIDI message by writing the bytes to the Serial interface. The Serial interface is typically connected to a MIDI output device or a computer running MIDI software.

The MIDI message consists of three bytes: the status byte indicates the type of message (e.g., Note On, Note Off, Control Change), and the data bytes carry additional information

## Software

Hairless MIDI and LoopMIDI are software tools commonly used together to establish MIDI communication between applications and devices on a computer. Here's some information about each of them:

### 1. Hairless MIDI:
   Hairless MIDI is a MIDI-over-Serial bridge application. It allows you to create a virtual serial port connection between MIDI-enabled applications and devices that communicate over serial ports. Hairless MIDI acts as a bridge, converting MIDI data into serial data and vice versa. This is useful when you want to connect MIDI-enabled hardware or software to applications that communicate through serial ports.

![hairlessMidi](https://github.com/e-for-eshaan/MIDI-Controller/assets/76566992/b16ab7d5-3368-4e91-b89b-def39ed61b21)


Hairless MIDI provides features such as baud rate selection, MIDI message logging, and the ability to filter or transform MIDI messages. It's compatible with various platforms including Windows, macOS, and Linux.

### 2. LoopMIDI:
   LoopMIDI is a virtual MIDI driver software. It creates virtual MIDI ports on your computer, allowing MIDI data to be routed between applications internally. With LoopMIDI, you can create multiple virtual MIDI ports, which can be used by different MIDI-enabled applications to communicate with each other.

![loopMidi](https://github.com/e-for-eshaan/MIDI-Controller/assets/76566992/1564aa4f-9172-43d4-b200-60292d8cfdf9)


LoopMIDI simplifies the process of connecting MIDI-enabled applications that need to exchange MIDI messages. You can set up virtual MIDI ports in LoopMIDI and configure applications to send and receive MIDI data through these ports.

By using Hairless MIDI and LoopMIDI together, you can establish MIDI communication between applications that communicate over serial ports and applications that use virtual MIDI ports. This allows for flexible and convenient integration of MIDI-enabled software and hardware on your computer.

<br/>

![DAW](https://github.com/e-for-eshaan/MIDI-Controller/assets/76566992/d4ff2a3e-629f-4f48-beb2-0e2b8c9e030f)

