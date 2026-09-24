#  Bluetooth Based Secure Locker System with Access Login

A **Bluetooth Based Secure Locker System with Access Login** is an embedded security project designed to provide controlled access to a locker using **Bluetooth communication, password authentication, and an LPC2148 microcontroller**.

The user can enter the login password through a Bluetooth-enabled mobile application. The system verifies the password and allows access only to an authorized user.

##  Features

*  Secure password-based login
*  Bluetooth-based user authentication
*  Access login system
*  LCD display for status messages
*  Password storage using I2C EEPROM
*  UART communication with HC-05
*  Access granted after successful authentication
*  Access denied for incorrect password
*  LPC2148-based embedded system

##  Hardware Requirements

* LPC2148 Microcontroller
* HC-05 Bluetooth Module
* 16x2 LCD Display
* I2C EEPROM
* Electronic Lock / Relay
* Power Supply
* Connecting Wires
* Android Smartphone

##  Software Requirements

* Keil µVision
* Embedded C
* Flash Magic / ISP Programmer
* Bluetooth Control Application

##  Technologies Used

| Technology | Purpose                 |
| ---------- | ----------------------- |
| Embedded C | Firmware development    |
| LPC2148    | Main microcontroller    |
| HC-05      | Bluetooth communication |
| UART       | Serial communication    |
| I2C        | EEPROM communication    |
| LCD        | User interface          |
| EEPROM     | Password storage        |

##  Working Principle

The **Bluetooth Based Secure Locker System with Access Login** is an embedded security system developed using the **LPC2148 ARM7 microcontroller**. The system provides controlled access to a locker by combining **Bluetooth communication, UART, password authentication, I2C EEPROM storage, LCD interfacing, and an electronic locking mechanism**.

The complete working process is divided into initialization, Bluetooth communication, password reception, password verification, and locker control.

### 1. System Initialization

When the system is powered ON, the LPC2148 microcontroller initializes all the required peripherals and modules.

The following peripherals are configured:

* **UART** – for communication between the LPC2148 and HC-05 Bluetooth module.
* **I2C** – for communication with the external EEPROM.
* **LCD** – for displaying system and authentication status.
* **GPIO pins** – for controlling the locker mechanism, buzzer, and other peripherals.
* **Security module** – for handling password authentication and access control.

After initialization, the LCD displays the welcome/login information and the system waits for the user to establish a Bluetooth connection.

### 2. Bluetooth Connection

The user connects an Android smartphone to the **HC-05 Bluetooth module**.

The HC-05 acts as a wireless serial communication interface between the mobile phone and the LPC2148.

The communication path is:

```text
Android Mobile
      │
      │ Bluetooth
      ▼
    HC-05
      │
      │ UART
      ▼
   LPC2148
```

The user can enter the required password using the Bluetooth control application.

### 3. Password Transmission Through UART

When the user enters the password in the mobile application, the password is transmitted wirelessly to the HC-05 module.

The HC-05 converts the received Bluetooth data into serial data and sends it to the **UART receiver of the LPC2148**.

The LPC2148 receives the password character by character through UART and stores the received characters in a temporary buffer.

For example:

```text
User enters:
1234

UART receives:
'1' → '2' → '3' → '4'
```

After receiving the complete password, the microcontroller starts the authentication process.

### 4. Password Storage Using I2C EEPROM

The authorized password is stored in an external **I2C EEPROM**.

The EEPROM is used because it is **non-volatile memory**, which means the stored password remains available even when the main power supply is switched OFF.

The LPC2148 communicates with the EEPROM using the two-wire I2C interface:

```text
LPC2148                    I2C EEPROM
   │                           │
   ├──── SDA ──────────────────┤
   │                           │
   └──── SCL ──────────────────┤
                               │
                              GND
```

Where:

* **SDA – Serial Data**
* **SCL – Serial Clock**

The LPC2148 acts as the I2C master and accesses the EEPROM to read the stored password.

### 5. Password Verification

Once the password is received through Bluetooth, the LPC2148 reads the authorized password from the EEPROM.

The microcontroller then compares:

```text
Password entered by user
          VS
Password stored in EEPROM
```

The comparison is performed character by character.

For example, if the stored password is:

```text
1234
```

and the user enters:

```text
1234
```

the characters match:

```text
1 = 1  ✓
2 = 2  ✓
3 = 3  ✓
4 = 4  ✓
```

Therefore, authentication is successful.

If even one character is different, authentication fails.

Example:

```text
Stored Password : 1234
Entered Password: 1254

1 = 1  ✓
2 = 2  ✓
5 ≠ 3  ✗
```

The system therefore denies access.

### 6. Successful Authentication

If the entered password matches the password stored in EEPROM, the LPC2148 grants access to the locker.

The LCD displays:

```text
ACCESS OK
```

The microcontroller then generates the required control signal to activate the locker mechanism.

The control sequence is:

```text
Correct Password
       │
       ▼
   LPC2148
       │
       ▼
Control Signal
       │
       ▼
Relay / Motor / Lock Mechanism
       │
       ▼
   Locker Opens
```

Thus, only a user providing the correct password can activate the locker-opening mechanism.

### 7. Incorrect Password

If the password entered by the user does not match the password stored in EEPROM, the LPC2148 rejects the authentication request.

The locker-opening mechanism is not activated.

The LCD can indicate the failed authentication status:

```text
ACCESS DENIED
```

The system then remains in the locked state and waits for another authentication attempt.

The basic logic is:

```text
              Password Received
                     │
                     ▼
             Read EEPROM Password
                     │
                     ▼
              Compare Passwords
                     │
             ┌───────┴────────┐
             │                │
          MATCH            NO MATCH
             │                │
             ▼                ▼
        ACCESS OK       ACCESS DENIED
             │                │
             ▼                ▼
       Open Locker      Keep Locker Locked
```

### 8. LCD Status Display

The **16×2 LCD** provides a local user interface and displays the current system status.

Depending on the operation, the LCD can display messages such as:

```text
BLUETOOTH SECURE LOCKER SYSTEM
```

```text
WAITING FOR BT PWD
```

```text
ACCESS OK
```

```text
ACCESS DENIED
```

This allows the user to understand the current state of the authentication process without directly accessing the microcontroller.

### 9. Security and Alert Mechanism

The project also contains dedicated modules for **security and buzzer control**.

The buzzer can be used to provide an audible indication during important events such as authentication failure or other security-related conditions.

The security logic handles the password verification and determines whether the locker-opening operation should be allowed.

### 10. Locker Control

After successful authentication, the LPC2148 controls the output connected to the locker mechanism.

The microcontroller itself does not directly drive a high-current lock or motor. Instead, an appropriate **driver/relay interface** can be used between the LPC2148 and the locking mechanism.

The basic control flow is:

```text
LPC2148 GPIO
     │
     ▼
Driver / Relay
     │
     ▼
Electronic Lock
     │
     ▼
Locker State Changes
```

After the required access period, the locker can be returned to its locked state according to the implemented control logic.

### 11. Complete System Flow

The complete working of the project can be summarized as follows:

```text
                     POWER ON
                         │
                         ▼
               Initialize LPC2148
                         │
             ┌───────────┼───────────┐
             ▼           ▼           ▼
           UART         I2C         LCD
             │           │           │
             ▼           ▼           ▼
           HC-05      EEPROM      Display
             │           │
             │           │
             ▼           ▼
        Bluetooth     Stored
          Input       Password
             │           │
             └─────┬─────┘
                   ▼
            Receive Password
                   │
                   ▼
             Compare Password
                   │
             ┌─────┴─────┐
             │           │
          Correct      Incorrect
             │           │
             ▼           ▼
        ACCESS OK   ACCESS DENIED
             │           │
             ▼           ▼
       Activate Lock   Keep Locked
        Mechanism
             │
             ▼
       Locker Opens
```

### 12. Software Module Interaction

The firmware is organized into multiple modules to make the embedded application easier to develop, test, debug, and maintain.

```text
                    projectmain.c
                         │
       ┌─────────────────┼─────────────────┐
       │                 │                 │
       ▼                 ▼                 ▼
     UART              LCD              EEPROM
       │                 │                 │
       ▼                 ▼                 ▼
    HC-05            Display          Password
  Communication       Status           Storage
       │
       ▼
   Bluetooth
   Password
       │
       ▼
    Security
       │
       ├──────────────► Password Verification
       │
       ├──────────────► Access Control
       │
       ▼
     Motor / Lock
       │
       ▼
    Locker Access
```

The repository contains dedicated source and header files for modules including **Bluetooth, UART, LCD, EEPROM, keypad, menu, motor, buzzer, RTC, and security**, allowing the functionality to be separated into reusable components.

### 13. Overall Operation

The complete operation can therefore be summarized as:

1. Power ON the system.
2. LPC2148 initializes UART, I2C, LCD, GPIO, and other required peripherals.
3. LCD displays the initial login/welcome message.
4. User connects the smartphone to the HC-05 Bluetooth module.
5. User enters the authentication password through the Bluetooth application.
6. HC-05 receives the Bluetooth data.
7. HC-05 transfers the received data to LPC2148 through UART.
8. LPC2148 collects and processes the received password.
9. LPC2148 reads the authorized password from I2C EEPROM.
10. The received password is compared with the stored password.
11. If both passwords match, authentication is successful.
12. LCD displays **ACCESS OK**.
13. LPC2148 activates the locker control mechanism.
14. The locker is opened for authorized access.
15. If the passwords do not match, LCD displays **ACCESS DENIED**.
16. The locker remains locked and the system waits for another authentication attempt.

### 🔐 Core Working Concept

The security of the system is based on the following chain:

```text
Bluetooth Authentication
          ↓
      HC-05
          ↓
       UART
          ↓
      LPC2148
          ↓
    EEPROM Password
          ↓
    Password Compare
          ↓
    ┌─────┴─────┐
    ↓           ↓
  MATCH       NO MATCH
    ↓           ↓
ACCESS OK   ACCESS DENIED
    ↓
Locker Opens
```

This architecture combines **wireless communication, embedded processing, non-volatile password storage, user feedback, and physical access control** into a single embedded security system.



##  Hardware Block Diagram

<p align="center">
  <img src="https://raw.githubusercontent.com/kalyan-777/Bluetooth-Based-Secure-Locker-System-with-Access-Login/a90e7532495e3d0f17da85865c0406e18cb6938d/block_diagram.jpg" alt="Hardware Block Diagram" width="800">
</p>

##  System Flow

```text
              POWER ON
                  │
                  ▼
          Display Login
                  │
                  ▼
       Connect HC-05 Bluetooth
                  │
                  ▼
          Enter Password
                  │
                  ▼
        Receive Through UART
                  │
                  ▼
        Compare With EEPROM
                  │
           ┌──────┴──────┐
           │             │
        Correct        Incorrect
           │             │
           ▼             ▼
      ACCESS OK      ACCESS DENIED
           │
           ▼
      Open Locker
```

##  Project Structure

```text
Bluetooth-Based-Secure-Locker-System-with-Access-Login/
│
├── Source/
│   ├── main.c
│   ├── uart.c
│   ├── lcd.c
│   ├── i2c.c
│   └── eeprom.c
│
├── Header/
│   ├── uart.h
│   ├── lcd.h
│   ├── i2c.h
│   └── eeprom.h
│
├── Images/
│   ├── hardware.jpg
│   ├── circuit.jpg
│   ├── lcd.jpg
│   └── bluetooth-app.jpg
│
└── README.md
```

> Modify the folder names above if your GitHub repository uses different file names or folders.

##  Project Images


### Circuit 

![Circuit 1](https://raw.githubusercontent.com/kalyan-777/Bluetooth-Based-Secure-Locker-System-with-Access-Login/a6337519b53b74d1d0f32c31e85abd5938221bf6/circuit1.jpg)


![Circuit 2](https://raw.githubusercontent.com/kalyan-777/Bluetooth-Based-Secure-Locker-System-with-Access-Login/0a956078638f535f413a9b73a7999923ce64db3a/circuit2.jpg)


![Circuit 3](https://raw.githubusercontent.com/kalyan-777/Bluetooth-Based-Secure-Locker-System-with-Access-Login/6e2e008163f53a430d16af409dfe20bae66872f3/circuit3.jpg)


![Circuit 4](https://raw.githubusercontent.com/kalyan-777/Bluetooth-Based-Secure-Locker-System-with-Access-Login/36de40e3c7a5e846308508b0ee66dcd2d0991952/circuit4.jpg)



![Circuit 5](https://raw.githubusercontent.com/kalyan-777/Bluetooth-Based-Secure-Locker-System-with-Access-Login/96c7cf20e917542a2d6b5f5b17fcfd551536ee5c/circuit_5.jpg)



![Circuit 6](https://raw.githubusercontent.com/kalyan-777/Bluetooth-Based-Secure-Locker-System-with-Access-Login/34038e9bc1caa6ec521b1eca102f3105b80fcf46/circuit6.jpg)

##  Applications

*  Smart lockers
*  Home security systems
*  Office lockers
*  Laboratory security
*  Educational institutions
*  Industrial access control

##  Future Enhancements

* Fingerprint authentication
* RFID authentication
* OTP-based login
* Mobile application with improved UI
* Multiple user accounts
* Failed-login security lockout
* IoT/cloud monitoring
* Security notifications

**Learning Outcomes**

Through this project, the following concepts can be learned:

* LPC2148 microcontroller programming
* Embedded C programming
* UART communication
* Bluetooth communication
* I2C protocol
* EEPROM read/write operations
* LCD interfacing
* Password authentication
* Embedded system debugging

##  Author

**Kalyan Naspuri**

B.Tech – Electronics and Communication Engineering

##  License

This project is created for **academic and educational purposes**.
