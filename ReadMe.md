# _I2C communication with the ADS1115 with ESP-01S using the ESP8266 SDK (ECNG 3006 Lab 1)_

# 3006 Lab 1 Repository 


For each exercise, ensure that the output file, the appropriately commented source files, and the final binary files, are part of your github repository.

<ol>
    <li>Create a new project based on the ESP8266 SDK example titled "hello_world", and ensure that the code is sync'd with github. Adjust the example so that: 
        <ol>
            <li>Replace the "hello world" message with a message that includes your name and ID#.</li>
            <li>Replace the number of seconds to restart with the last two digits of your ID# modulo 15. e.g. for ID#8169875234 the number of seconds would be 34 modulo 15 = 4.
            <br> Capture the output of this program into a file named "lab1_q1_xxxxxxxxx.out" where xxxxxxxxx is your ID#
            </li>
        </ol>
    </li>
    <li>Create a new project based on the RTOS SDK example titled "gpio". This example is setup to use 4 pins, 2 inputs and 2 outputs. Adjust the example so that:
        <ol>
            <li>Only a single input and a single output are specified, and the input and output pins selected consistent with available pins on the ESP-01S</li>
            <li>A single handler is installed and used for the input on the falling edge</li>
            <li>A sempahore is passed from the ISR instead of a message</li>
        </ol>
    </li>
    <li>Capture the output of this program into a file named "lab1_q2_xxxxxxxxx.out" where xxxxxxxxx is your ID# 
    Create a new project based on the RTOS SDK example titled "i2c". This example is setup to use the MPU6050 - adjust the example to use the ADS1115 by: 
        <ol>
            <li>Configure the #defines associated with the SCL and SDA lines to be consistent with available pins on the ESP-01S and verify that the master_init routine is appropriate.</li>
            <li>Remove the #defines associated with the MPU6050, determine the I2C address of the ADS1115 and the ADS1115 registers to be configured/read/written on the ADS1115 to allow a single-sided analog input (with no explicit voltage reference lines) on channel 0, create new #defines and adjust the master_device_read, master_device_write, and master_device_init routines accordingly.</li>
            <li>Replace i2c_task_example with an example that will read and report the analog signal connected to channel 0 of the ADC at appropriate intervals.
                <br>Capture the output of this program into a file named "lab1_q3_xxxxxxxxx.out" where xxxxxxxxx is your ID#</li>
        </ol>
    </li>
</ol>

# _I2C Example_

* This example will show you how to use I2C module:
 
    * read external i2c sensor, here we use a MPU6050 sensor for instance.

## Pin assignment

* master:
    * GPIO14 is assigned as the data signal of i2c master port
    * GPIO2 is assigned as the clock signal of i2c master port

## How to use example

### Hardware Required

* Connection:
    * connect sda/scl of sensor with GPIO14/GPIO2
    * no need to add external pull-up resistors, driver will enable internal pull-up resistors.

### Configure the project

```
make menuconfig
```

* Set serial port under Serial Flasher Options.


### Build and Flash

Build the project and flash it to the board, then run monitor tool to view serial output:

```
make -j4 flash monitor
```

(To exit the serial monitor, type ``Ctrl-]``.)

See the Getting Started Guide for full steps to configure and use ESP-IDF to build projects.

## Example Output  

```
I (0) gpio: GPIO[14]| InputEn: 0| OutputEn: 1| OpenDrain: 1| Pullup: 1| Pulldown: 0| Intr:0
I (0) gpio: GPIO[2]| InputEn: 0| OutputEn: 1| OpenDrain: 1| Pullup: 1| Pulldown: 0| Intr:0
I (0) main: *******************

I (0) main: who_am_i: 68

I (0) main: TEMP: 26.51

I (0) main: sensor_data[0]: -1288

I (0) main: sensor_data[1]: 8796

I (0) main: sensor_data[2]: 11088

I (0) main: sensor_data[3]: -3408

I (0) main: sensor_data[4]: -223

I (0) main: sensor_data[5]: 67

I (0) main: sensor_data[6]: -11

I (0) main: error_count: 0

I (0) main: *******************

I (0) main: who_am_i: 68

I (0) main: TEMP: 26.55

I (0) main: sensor_data[0]: -1224

I (0) main: sensor_data[1]: 8748

I (0) main: sensor_data[2]: 11084

I (0) main: sensor_data[3]: -3392

I (0) main: sensor_data[4]: -318

I (0) main: sensor_data[5]: 235

I (0) main: sensor_data[6]: 21

I (0) main: error_count: 0

```
