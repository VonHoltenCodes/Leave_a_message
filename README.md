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

### Components
- **Microcontroller**: Teensy 3.x/4.x (Teensy 4.1 recommended for optimal performance)
- **Display**: RA8875-based TFT display (800x480 resolution) with capacitive touch
- **Audio Hardware**: SGTL5000 audio codec (Teensy Audio Shield or equivalent)
- **Storage**: SD card module (at least 4GB recommended)
- **Microphone**: Dynamic microphone (preferred over condenser for better noise rejection)
- **Audio Output**: Speakers or headphone output
- **Power Supply**: 5V power supply with sufficient current capacity (500mA minimum)

### Pinout Configuration

#### RA8875 TFT Display Connections
| Pin Function | Teensy Pin | Notes |
|--------------|------------|-------|
| CS           | 5          | Chip select for display |
| RESET        | 9          | Display reset line |
| INT          | 2          | Touch interrupt (important for responsiveness) |
| MOSI         | 26         | SPI data output - non-standard pin! |
| SCLK         | 27         | SPI clock - non-standard pin! |
| MISO         | 39         | SPI data input - non-standard pin! |

#### SD Card Connections
| Pin Function | Teensy Pin | Notes |
|--------------|------------|-------|
| CS           | 10         | Chip select for SD card |
| MOSI         | 11         | SPI data output |
| SCK          | 13         | SPI clock |

#### Audio Connections
- The SGTL5000 audio codec connects via I2S and I2C interfaces
- Microphone input connects to the audio shield's mic input
- **Important**: A dynamic microphone is strongly recommended over condenser types, as it provides better noise rejection in public installation environments and doesn't require phantom power
- Audio gain is set to 40dB in software to optimize for typical speaking volume

#### Power Requirements
- The system requires a stable 5V power supply
- Current requirements increase during audio recording/playback
- For long-term installation, a regulated power supply with battery backup is recommended

## Features

- Audio message recording and playback
- Message storage and session management
- Touch-based user interface
- Audio level monitoring for optimal recording
- Countdown timer for recording duration
- Multiple message storage

![Audio Level Monitoring](screenshots/LAM_Audio-level.JPEG)

## Session Management

The project implements an intelligent session management system designed for long-term installations and power cycles:

- **Automatic Session Creation**: Each time the device powers on, it automatically creates a new session folder for storing messages, or continues an existing session if it's nearly empty.

- **Power Cycle Handling**: When power is lost and restored, the system creates new session folders to ensure no message data is overwritten or corrupted.

- **Folder Structure**: Messages are organized in numbered folders (e.g., `/messages`, `/messages2`, `/messages3`), with each new power cycle potentially creating a new session folder.

- **Session Continuity**: If a previous session folder contains fewer than 3 messages, the system will continue using it rather than creating a new folder. This prevents having many nearly-empty session folders.

- **Message Preservation**: The session system ensures that even in environments with frequent power interruptions, all recorded messages are preserved and properly organized.

## Installation

### Software Setup
1. Install the Arduino IDE and Teensyduino add-on (https://www.pjrc.com/teensy/teensyduino.html)
2. Install the following libraries through the Arduino Library Manager:
   - Audio (Teensy Audio Library)
   - Wire
   - SPI
   - SD
   - RA8875 (for the TFT display)
3. Connect your Teensy to your computer via USB
4. Select the appropriate Teensy board from the Arduino IDE Tools menu
5. Set the USB Type to "Serial" in the Tools menu
6. Upload the `Leave_a_message.ino` sketch to your Teensy

### Hardware Assembly
1. Mount the RA8875 display in an appropriate enclosure
2. Connect the Teensy Audio Shield to the Teensy microcontroller
3. Wire the RA8875 display to the Teensy according to the pinout table above
4. Connect your dynamic microphone to the microphone input on the Audio Shield
5. Connect speakers or headphones to the audio output
6. Insert a formatted SD card into the SD card slot
7. Connect power to the system

### Physical Installation Tips
1. For public installations, consider these recommendations:
   - Mount the display at a comfortable height (around eye level for average adults)
   - Position the microphone at an appropriate distance from the display (about 8-12 inches)
   - Use shielded cables for all audio connections to minimize interference
   - Include clear signage explaining how to use the system
   - Secure all components to prevent tampering
   - Consider weather protection if installed in a semi-outdoor environment

2. First-time startup:
   - The system will automatically create a messages folder on the SD card
   - Follow the on-screen instructions to interact with the system

## Usage

The system allows users to:
- Record new audio messages (up to 60 seconds per message)
- Browse and play back previously recorded messages
- Navigate through multiple recording sessions
- Monitor audio levels during recording
- View recording countdown timer

## Technical Details

### Recording Process
1. The system captures audio at 44.1kHz with 16-bit resolution (CD quality)
2. Audio is buffered through the SGTL5000 codec and saved to SD card
3. WAV files are created with proper headers for universal compatibility
4. Audio level monitoring provides visual feedback during recording
5. Each message is timestamped with a unique identifier

### File Format
- Standard WAV files (uncompressed PCM audio)
- 44.1kHz sample rate, 16-bit depth, mono channel
- Compatible with any audio player or software
- Files are named using a timestamp format: `msg_MMDD_HHMM_X.wav`

### Power Management
- The system is designed to handle power interruptions gracefully
- No data loss occurs when power is cut unexpectedly
- Sessions are managed to organize recordings across power cycles
- SD card writes are properly finalized to prevent data corruption

## License

This project is open source and available for educational and recreational purposes.

## Author

Created by VonHoltenCodes.