Vehicle-accident-alert--system

Accident detection system using Arduino, MPU6050, SW-420, GSM, GPS
Vehicle-Accident-Alert-System

A real-time embedded system that detects vehicle crashes and rollovers, sends location via SMS, makes emergency calls, and shuts down the motor — designed and built by a Mechanical Engineering student with no prior experience in electronics or IoT.

  ---
  
 What It Does

- Detects **crashes** using SW420 vibration sensor
- Detects **rollovers** using MPU6050 accelerometer
- **Cuts off vehicle motor** using 5V relay (FOR DEMONSTRATION PURPOSE - ENGINE KILL)
- Sends **SMS with live GPS location** (Google Maps link) via GSM SIM900A
- Makes an **emergency phone call**
- Displays status on **16x2 I2C LCD**

  ---

Hardware Used

| Component         | Purpose                                      |
|------------------|----------------------------------------------|
| Arduino UNO R3    | Main controller                             |
| MPU6050           | Rollover detection (tilt/acceleration)       |
| SW420             | Crash detection (vibration sensor)           |
| SIM900A GSM       | SMS and phone call alerts                    |
| NEO-6M GPS        | Get live coordinates                         |
| I2C 16x2 LCD      | System feedback display                      |
| 5V Relay          | Motor cutoff after accident (demonstrating engine kill)                 |
| LM2596 Converter  | Power regulation from battery                |
| Buzzer            | Local audible alert                         |
| DC Motor          | Simulated vehicle load                      |


 What I Learned

- Sensor interfacing and real-time data handling
- Managing multiple serial devices (GSM + GPS)
- Debugging hardware failures, relay misfires, GPS timeouts
- Power handling with external modules (buck converters)
- Importance of testing in real-world environments

---

 Challenges Faced

- GPS failed in enclosed areas or under trees
- GSM coverage was unreliable in low-network zones
- Over-sensitive vibration sensor triggered false alarms
- Initial relay logic caused motor to cut unexpectedly

---

Future Improvements

- Replace GPS with **GPS+GLONASS** (NEO-M8N) for better signal
- **SD card logging** for black-box style accident data
- Smarter accident detection logic (using combined sensor patterns)
- Create a **compact, enclosed model** for direct use in vehicles
- Add battery level monitoring + LED fault indication

---

Final Thoughts

This project may not be groundbreaking, but it reflects **effort, trial and error, and learning by doing**. As a **first-year Mechanical Engineering student**, I had no background in electronics, IoT, or AI — but I took it up to learn and solve something real.

And now I ask...

What could a 1st-year Mechanical Engineering student with no prior knowledge of electronics, IoT, or AI possibly build?**  
Apparently… this. 😂

---

Project Author
Name: Ahamed Ibrahim Mohamed Haniffa 
College: B.S. Abdur Rahman Crescent Institute of Science and Technology  
Department: B.Tech Mechanical Engineering  
GitHub: https://github.com/AhamedIbrahim05


#Arduino #EmbeddedSystems #MechanicalEngineering #IoT #GSM #GPS #CrashDetection #StudentProject #MPU6050 #LearningByDoing
