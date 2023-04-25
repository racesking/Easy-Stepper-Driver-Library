# Easy Stepper Driver Library for Arduino

The Easy Stepper Driver Library is a user-friendly, efficient, and robust Arduino library designed to simplify the control of stepper motors using various stepper driver modules. This library makes it easy to interface with popular stepper motor drivers, including A4988, DRV8825, and others, providing smooth and precise motor control for a wide range of applications.

## Features

- Simple and intuitive API for stepper motor control
- Supports various stepper driver modules, including A4988, DRV8825, and more
- Acceleration and deceleration support for smooth motion
- Configurable step modes: Full-step, half-step, micro-stepping
- Adjustable speed and acceleration settings
- Comprehensive example sketches to help you get started quickly

## Installation

1. Download the library as a ZIP file or clone this repository to your local machine.
2. Open the Arduino IDE.
3. Go to `Sketch` > `Include Library` > `Add .ZIP Library` and select the downloaded ZIP file or the cloned repository folder.
4. The library should now be installed and available under `Sketch` > `Include Library` > `Easy Stepper Driver Library`.


## Library Overview

This library is used to control one or more stepper motors. It requires a stepper driver board that has a Step and Direction interface. The motors are accelerated and decelerated as they travel to the final position. This driver supports changing the target position, speed, or rate of acceleration while a motion is in progress.

Because the library allows making changes while moving, it cannot generate as fast of a step rate as a driver that requires each motion to complete. To step faster, see the companion Arduino stepper library: SpeedyStepper.

This library can generate a maximum of about 7,000 steps per second using an Arduino Uno. Assuming a system driving only one motor at a time, in full step mode, with a 200 steps per rotation motor, the maximum speed is about 35 RPS or 2100 RPM (most stepper motors cannot go this fast). Driving one motor in half step mode, a maximum speed of 17 RPS or 1050 RPM can be reached. In quarter step mode, about 9 RPS or 525 RPM. Running multiple motors at the same time will reduce the maximum speed. For example, running two motors will reduce the step rate by half or more.

This stepper motor driver is based on Aryeh Elderman's paper "Real Time Stepper Motor Linear Ramping Just By Addition and Multiplication". See: www.hwml.com/LeibRamp.pdf

It has advantages and disadvantages over David Austin's method. The advantage is that it is faster, meaning you can generate more steps/second. The disadvantage is that the speed ramping while accelerating and decelerating is less linear. This is likely to only be a problem when coordinating multiple axes that all need to start and finish motions precisely at the same time.

## Usage

1. Include the library in your sketch:

```cpp
#include <EasyStepperDriver.h>
```

2. Create an instance of the `EasyStepperDriver` class, specifying the required pins:

```cpp
EasyStepperDriver stepper(STEP_PIN, DIR_PIN, ENABLE_PIN); // Replace with your pin numbers
```

3. In the `setup()` function, initialize the stepper motor and configure its settings:

```cpp
void setup() {
  stepper.begin();
  stepper.setSpeed(100); // Steps per second
  stepper.setAcceleration(50); // Steps per second squared
}
```

4. Use the library functions to control the stepper motor in the `loop()` function:

```cpp
void loop() {
  stepper.move(200); // Move 200 steps forward
  delay(1000);
  stepper.move(-200); // Move 200 steps backward
  delay(1000);
}
```

For more examples and advanced usage, check the `examples` folder in this repository.

## Contributing

Contributions to the library are welcome. If you'd like to add support for more stepper drivers, improve existing features, or suggest any enhancements, feel free to open an issue or submit a pull request.

## License

This project is released under the MIT License. See the `LICENSE` file for more details.