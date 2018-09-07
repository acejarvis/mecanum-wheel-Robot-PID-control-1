mecanum-wheel-Robot-PID-control
====
MPU-9250 sensor setup on Raspberry Pi 3B
----
1. Connect `SCL` & `SDA` pin to pin5 & pin3 of Raspberry Pi, then connect `Vcc` & `Ground` pin to the 3.3V power pin(pin1) & Ground pin of Raspberry Pi<br>
![connection](https://github.com/qooiprww/mecanum-wheel-Robot-PID-control/blob/master/raspberry-pi-mpu6050-six-axis-gyro-accelerometer-5.jpg "MPU-9250")
2. 
First we set up a folder for the project in the /home/pi directory and get the i2c tools installed
```Bash 
mkdir jbc
cd jbc
mkdir scripts
sudo apt-get install i2c-tools
```
Click the Menu in the top Left Corner, go to Prefrences->Raspberry Pi Configuration->Interfaces and enable i2c (this will require a reboot).<br>
3.
```Bash
sudo i2cdetect -y 1
   ```
If the number 68 is in the grid that displays, mpu is detected.<br>
Then install cmake for building the sensor's library
```Bash 
sudo apt-get install cmake
```
Install python to setup the develop environment
```Bash 
sudo apt-get install python-dev
```
Install Octave to calibrate the sensor
```Bash 
sudo apt-get install octave
```
Next, get the RTIMULib Library from Github
```Bash 
git clone https://github.com/richards-tech/RTIMULib2.git
cd RTIMULib2/Linux/RTIMULibCal
make -j4
sudo make install
```
The last thing is to setup our working directory
```Bash 
cp -r /home/pi/jbc/RTIMULib2/RTEllipsoidFit/ /home/pi/jbc/
```
4. Calibrating the MPU-9250 on the Raspberry Pi
Change to the RTEllipsoidFit folder and run RTIMULibCal:
```Bash 
cd /home/pi/jbc/RTEllipsoidFit/
RTIMULibCal
```
Then follow the instructions to calibrate the sensor.<br>
After finished, copy the sonser data file to our working dictionary
```Bash 
cp RTIMULib.ini /home/pi/jbc/scripts/
```
5. Down the [imu2.py]() file
```Bash 
cp RTIMULib.ini /home/pi/jbc/scripts/
```
