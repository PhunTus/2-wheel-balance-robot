# 📧 Contact
Co-author:
- **Phung Van Tu** - [Phungtu1310@gmail.com](mailto:Phungtu1310@gmail.com)
- **Le Minh Thuan** - [Leminhthuan2004@gmail.com](mailto:Leminhthuan2004@gmail.com)
# 🤖 2-wheel-balance-robot
- All source of project
# 💾 Discription
- Using some controller: PID, Karmal filter, low-pass mask, high-pass mask,....
The input of system is angle value from MPU6050 Sensor (feedback signal)
and the output is the value of PWM that control the speed and angle of motors.
- Robot can be controlled through Bluetooth connection using module HC-05.
# 🧰 Parts
- Arduino Nano
- Extend module for Stepper driver CNC shield V3
- Step driver A4988
- Step motor NEMA 17
- 12-Volt battery
- Frame of robot
# 🦾 Working Principles
- This will work like an inverted pendulum. If the body of bot move forward,   
the wheels must run forward to maintain the balance - otherwise, it will fall down.
# 🧠PID Controller 
- PID stands for 3 words:
- P: Proportional
- I: Integral
- D: Derivative
- A PID controller is a feedback control algorithm that helps the output value
of system(Output) to reach a desired value (Setpoint) by adjusting the input control
signals.
- In this system, the input control signal is calculated (I'll show with C++ language):
#####  float error = setpoint -  input;  // cal the error between current angle and desired angle(0 degree)
#####  float errSum += error * dt;   // cal the integral of error
#####  float Derror = (error - lastErr) / dt;   // cal the derivative of error 
##### output = Kp * error + Ki * errSum + Kd * Derror; //  Sum of P, I, and D components --> The speed of Robot
#### <img width="489" height="87" alt="image" src="https://github.com/user-attachments/assets/313fa254-d164-4157-b8a9-5a66d238bba7" /> --> The general formula of PID
# 💻Kalman Filter
- Using SimpleKalmanFilter.h from Arduino.
- Specifically, I'll initialize a function with three arguments:
##### SimpleKalmanFilter  kalman(measurementNoise,  estimationErr,  processNoise) ;  
- And then, the angle is corrected with Kalman:
#####    float kalmanAngle = kalman.updateEstimate(acceAngle,  gyroRate,   dt)  ;
#####    input = kalmanAngle  ;
