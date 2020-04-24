# DEMO - Light sensors {#light-sensors status=draft}

## Hardware setup {#light-sensors-hardware}

<div class='requirements' markdown="1">

Requires: A fully operational Watchtower 
Results: Accurate measure of the light field of the Autolab

</div>

To see how you have to assamble and plug in the RGB-sensor have a look at section 2.21 to 2.24: [Hardware setup RGB-sensor](#watchtower-hardware-assembly-WT19-A). 

Note: **I/O error** : If you get an Input/Output error probably one of your pins is demaged. So use an alternative pin configuration: https://www.raspberrypi.org/documentation/usage/gpio/


## Software setup {#light-sensors-software}

<div class='requirements' markdown="1">
Requires: A sensor which is correctly setup on a running watchtower.
Ideally an external light sensor that measures luminescence that can be used as reference.

Result: An environment where you can control the light intensity, it can also be very small (try to use two light intensities below and above the operating point).
</div>

### Calibration
To calibrate the sensor we need to measure the light at two different intensities in order to be able to make a linear approximation. You are going to give as input twice a value of the real intesity of light. For this you are going to need an external light sensor as reference with which you can measure the luminescence next to sensor you want to callibrate.

To do so run the demo and follow the steps of the instruction provided on the console.

    laptop $ dts duckiebot demo --duckiebot_name WATCHTOWER_NAME --demo_name light_sensor_calibration --package_name light_sensor_calibration --image duckietown/dt-light-sensor:daffy-arm32v7 --debug


### Sensor
Run the following demo:

    laptop $ dts duckiebot demo --duckiebot_name WATCHTOWER_NAME --demo_name light_sensor --package_name light_sensor --image duckietown/dt-light-sensor:daffy-arm32v7

the Sensor is publishing a message with the information of the intensity of red,blue and green light, the calculated value of the total light intensity and real_lux, whicht takes our callibration into account. 





