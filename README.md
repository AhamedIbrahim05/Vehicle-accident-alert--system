# Vehicle Accident Detection and Alert System (IoT)

The Vehicle Accident Detection and Alert System is an embedded IoT-based safety prototype designed to automatically detect vehicle accidents and notify emergency contacts with precise location details. The system integrates inertial sensing, vibration detection, GPS positioning, and GSM communication to reduce response time during road accidents.

This project focuses on practical implementation of embedded systems concepts, real-time sensor monitoring, and reliable communication under constrained hardware conditions.

---

## Project Overview

Road traffic accidents often remain unreported for critical minutes, particularly in remote or low-traffic areas. Delays in emergency response significantly increase the risk of severe injury or fatality. Conventional reporting methods rely heavily on human intervention, which may not be possible immediately after an accident.

This project addresses the problem by implementing an automated accident detection mechanism using onboard sensors. The system continuously monitors vehicle motion parameters and vibration levels. When abnormal conditions indicative of a collision or rollover are detected, the system automatically acquires the vehicle’s GPS coordinates and transmits an alert message via GSM to predefined emergency contacts.

---

## Functional Description

The system performs the following functions:

- Detects high-impact collisions using an SW-420 vibration sensor  
- Identifies vehicle rollovers and abnormal orientation using MPU6050 accelerometer data  
- Demonstrates engine cutoff functionality using a 5V relay (prototype-level demonstration only)  
- Automatically sends SMS alerts containing live GPS coordinates and a Google Maps link  
- Initiates an emergency phone call to a predefined contact number  
- Displays real-time system status and alerts on a 16×2 I2C LCD module  

---

## System Architecture

### Sensors
- **MPU6050**: Measures acceleration and angular motion to detect rollovers and sudden impacts  
- **SW-420 Vibration Sensor**: Detects high-magnitude vibrations associated with collisions  

### Controller
- **Arduino** microcontroller responsible for sensor interfacing, decision logic, and communication control  

### Communication Modules
- **GPS Module**: Provides real-time latitude and longitude data  
- **GSM Module (SIM900A or equivalent)**: Sends SMS alerts and initiates emergency calls  

### Detection Logic
- Threshold-based decision logic using acceleration magnitude and vibration intensity  
- Threshold values determined experimentally to balance sensitivity and false-positive reduction  

---

## Code Structure and Logic

The firmware is developed using Embedded C within the Arduino framework. The code is organized to ensure readability, modularity, and ease of debugging.

### Major Code Modules
- Sensor initialization and data acquisition  
- Accident detection algorithm  
- GPS data parsing and validation  
- GSM communication for SMS and call handling  
- LCD interface for system status feedback  

### Detection Workflow (Conceptual)

Read accelerometer and vibration sensor data  
If sensor values exceed predefined thresholds:  
→ Confirm abnormal motion or impact  
→ Acquire current GPS coordinates  
→ Send SMS alert with location details  
→ Initiate emergency phone call  

Sensor thresholds were tuned through repeated testing to minimize false triggers caused by normal road conditions.

---

## My Role and Contributions

- Integrated and calibrated inertial and vibration sensors  
- Designed and implemented the accident detection logic  
- Developed firmware for GSM-based SMS and call functionality  
- Implemented GPS data acquisition and location formatting  
- Conducted end-to-end hardware testing and functional validation  

---

## Technical Challenges

- Inconsistent GPS signal availability in indoor or low-coverage environments  
- False positives caused by road irregularities and sudden braking  
- Maintaining stable power delivery for continuous system operation  

These challenges were addressed through iterative testing, threshold adjustment, and hardware-level optimization.

---

## Results and Outcome

The prototype successfully detects simulated accident scenarios such as collisions and rollovers. Upon detection, the system reliably transmits GPS-based SMS alerts and initiates emergency calls, demonstrating the feasibility of automated accident reporting using low-cost embedded hardware.

---

## Technology Stack

- Arduino  
- Embedded C  
- MPU6050 Accelerometer and Gyroscope  
- SW-420 Vibration Sensor  
- GSM Communication Module  
- GPS Module  
- Internet of Things (IoT) concepts  

---

## Future Enhancements

- Integration of machine learning techniques to reduce false positives  
- Development of a mobile application for alert monitoring and acknowledgment  
- Cloud-based data logging and analytics for long-term accident analysis  

---

## Disclaimer

This project is a prototype developed for academic and learning purposes only.  

