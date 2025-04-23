# Leave a Message Arduino Project

An interactive Arduino project that allows users to leave and display messages on a touchscreen interface. Record audio messages that can be played back later!

![Leave a Message Idle Screen](screenshots/LAM_idle.JPEG)

## Overview

This project implements a message board functionality using an Arduino-compatible microcontroller. Users can leave audio messages that are stored and played back according to programmed criteria.

### Project Screens

| Recording Interface | Sessions Screen |
|:------------------:|:---------------:|
| ![Start Recording](screenshots/LAM_start-recording.JPEG) | ![Sessions](screenshots/LAM_Sessions.JPEG) |

| Countdown Screen | Message Saved |
|:----------------:|:-------------:|
| ![Countdown](screenshots/LAM_countdown.JPEG) | ![Message Saved](screenshots/LAM_message-saved.JPEG) |

## Hardware Requirements

- Arduino-compatible microcontroller (e.g., Arduino Uno, Teensy, ESP32)
- Display (LCD, OLED, or TFT screen for message display)
- Input method (buttons, keypad, or touchscreen)
- Optional: Storage module for message persistence

## Features

- Audio message recording and playback
- Message storage and session management
- Touch-based user interface
- Audio level monitoring for optimal recording
- Countdown timer for recording duration
- Multiple message storage

![Audio Level Monitoring](screenshots/LAM_Audio-level.JPEG)

## Installation

1. Connect the hardware components according to the pin definitions in the code
2. Upload the `Leave_a_message.ino` sketch to your Arduino-compatible board
3. Follow the on-screen instructions to interact with the system

## Usage

The system allows users to:
- Record new audio messages
- Browse and play back previously recorded messages
- Navigate through multiple recording sessions
- Monitor audio levels during recording
- View recording countdown timer

## License

This project is open source and available for educational and recreational purposes.

## Author

Created by VonHoltenCodes.