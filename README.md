# RFID and GPS-Based Access Control System

This project implements an access control system using RFID, GPS, and GSM modules. The system uses an RFID reader to detect user cards, a GPS module to track the device's location, and a GSM module to send SMS notifications. An LCD is used for user interaction, and a motor (dynamo) is controlled to represent locking and unlocking mechanisms.

---

## Components Used
1. **Arduino**
2. **MFRC522 RFID Module**
3. **LiquidCrystal_I2C LCD**
4. **AltSoftSerial Module**
5. **TinyGPS++ Library**
6. **SoftwareSerial Library**
7. **SIM800L GSM Module**
8. **Buzzer**
9. **Motor (Dynamo)** for Locking/Unlocking Mechanism

---

## Features
- **RFID Authentication**: Detects RFID cards to allow or deny access.
- **Lock/Unlock Mechanism**: Controls physical locking based on card authentication.
- **GPS Tracking**: Tracks the current location of the system.
- **SMS Alerts**: Sends the location link via SMS when a specific keyword is detected.
- **LCD Display**: Provides visual feedback to the user.

---

## Functionality Overview

### Setup
1. **Initialize Modules**: Configures the RFID reader, LCD, GPS, and GSM modules.
2. **Pin Configuration**: Sets up pins for the buzzer, locking mechanism, and serial communication.
3. **User Prompt**: Displays "Tempelkan kartu" (Place the card) on the LCD.

### Loop
- **Card Detection (`baca()`)**:
  - Checks if a new RFID card is present.
  - Reads the card's UID.
  - Matches the UID to predefined authorized cards.
    - **Authorized Card (UID: `63 54 09 1C`)**: Unlocks the system and tracks borrowing duration.
    - **Authorized Card (UID: `A5 22 77 53`)**: Locks the system and resets the duration.
    - **Unauthorized Card**: Triggers an access denied buzzer alert.

- **GPS and SMS (`GPS()` and `linkSms()`)**:
  - Retrieves current GPS coordinates and generates a Google Maps link.
  - Sends the location link via SMS when the "FIND" keyword is received.

---

## Functions

### `setuptrack()`
Initializes GPS and GSM modules.

### `GPS()`
Fetches the current GPS coordinates and constructs a Google Maps link.

### `linkSms()`
Handles SMS sending when a specific keyword is detected in incoming messages.

### `baca()`
Processes RFID card scanning and handles corresponding actions based on the card's UID.

### `hilang()`
Handles scenarios where the system is unlocked but no card is detected.

### `lock()`
Activates the locking mechanism by controlling the motor (dynamo).

### `unlock()`
Activates the unlocking mechanism by controlling the motor (dynamo).

### `off()`
Deactivates the motor (dynamo).

### `check()`
Monitors for card removal after initial detection.

---

## How to Use
1. Connect all components as specified in the code.
2. Upload the code to the Arduino.
3. Place an RFID card near the reader.
   - For authorized cards, the motor (dynamo) will activate to open or close the lock accordingly.
   - For unauthorized cards, access will be denied.
4. Use the SMS feature to request the device's location using the keyword "FIND".

---

## Notes
- **Predefined UIDs**: Update the code with your RFID card UIDs for authorized access.
- **SMS Configuration**: Replace the placeholder phone number with your own for SMS functionality.
- **GPS Accuracy**: Ensure the GPS module has a clear view of the sky for accurate location tracking.

---

## Dependencies
- [TinyGPS++ Library](https://github.com/mikalhart/TinyGPSPlus)
- [AltSoftSerial Library](https://www.pjrc.com/teensy/td_libs_AltSoftSerial.html)
- LiquidCrystal_I2C and MFRC522 libraries (available in the Arduino Library Manager).

---

## Troubleshooting
- **RFID Not Detected**: Check wiring and ensure proper placement of the card.
- **GPS Location Not Found**: Ensure the module has sufficient satellite visibility.
- **SMS Not Sent**: Verify GSM module signal strength and SMS configurations.
- **Buzzer Not Working**: Check connections and ensure the pin is correctly configured.

---

## License
This project is open-source and can be modified as per your requirements.

