# Seed-Plantation-Drone-Simulation

#### Install the package updates on your linux system:
`sudo apt-get update`

#### Install python2 if not already installed:
`sudo apt install python2` 

#### DroneKit-Python and the dronekit-sitl simulator are installed from pip on all platforms. On Linux you will first need to install pip and python-dev: 
`sudo apt-get install python-pip python-dev`
`pip install dronekit`

#### Install DroneKit – SITL:
`pip install dronekit-sitl -UI`

#### Install MAVProxy:
`pip install MAVProxy` 

#### Install APMPlanner2 
Download the latest deb file for your machine from: 
`firmware.ardupilot.org/Tools/APMPlanner` 
 
#### Open a terminal window and go to the location where you downloaded the .deb file from step 2 and type the following command: 
`sudo apt-get -f install`  
`sudo dpkg -i apm_planner*.deb` 

### Running the code 

#### Method 1:  Directly running the python scripts:
`python filename.py`   

#### Method 2: Run the APM Planner2 and minimize it.  Open 3 terminals and execute each of the following in each terminal: 
 
#### a) First run the DroneKit simulator with desired vehicle and its attributes. 
`dronekit-sitl copter --home=10.0,20.0,0,180` 

Above command runs the start the simulation with copter at home location (latitude = 10.0 and longitude = 20.0 in above command) and 0 and 180 are copter parameters like model etc. It starts the SITL connection at: tcp:127.0.0.1:5760  
 
#### b) Use MavProxy to replicate the connection to other links like: 
`mavproxy.py --master tcp:127.0.0.1:5760 --sitl 127.0.0.1:5501 --out 127.0.0.1:14550 --out 127.0.0.1:14551` 
APM Planner should automatically connect to one of the out links from above command. 
 
#### c) Now run the required python drone script drone_AUTO.py or drone_GUIDED.py as follows: 
 
`python drone_GUIDED.py --connect udp:127.0.0.1:14551` 
 
or 
 
`python drone_AUTO.py --connect udp:127.0.0.1:14551` 
Monitor the drone in APM Planner and terminal outputs. For detailed terminal outputs view the Master.log generated by the code.
