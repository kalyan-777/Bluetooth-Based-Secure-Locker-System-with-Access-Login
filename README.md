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

## 🔧 Technologies Used

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

1. Power ON the system.
2. The LCD displays the welcome/login message.
3. Connect the mobile phone to the **HC-05 Bluetooth module**.
4. Open the Bluetooth control application.
5. Enter the required login password.
6. The LPC2148 receives the password through UART.
7. The entered password is compared with the stored password.
8. If the password is correct, the system displays **"ACCESS OK"** on the LCD.
9. The electronic locker is activated/opened.
10. If the password is incorrect, access is denied.

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


![Circuit Diagram](https://raw.githubusercontent.com/kalyan-777/Bluetooth-Based-Secure-Locker-System-with-Access-Login/6c58cd8a3afd7e91de0b770cae5ad0ce60564bf1/circuit.jpg.png)

![Circuit 1](https://raw.githubusercontent.com/kalyan-777/Bluetooth-Based-Secure-Locker-System-with-Access-Login/bf966394ce5c30ad7e6d2d0c287f88182e39bb4f/circuit1.jpg.png)

![Circuit 2](https://raw.githubusercontent.com/kalyan-777/Bluetooth-Based-Secure-Locker-System-with-Access-Login/c14ddb0102dff372123ddbad9e17ba269d318174/circuit2.jpg.png)

![Circuit 3](https://raw.githubusercontent.com/kalyan-777/Bluetooth-Based-Secure-Locker-System-with-Access-Login/7780ec94d5c50b9181eae14a35bf6e29ffa0f6a5/circuit3.jpg.png)
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
