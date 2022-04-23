+++
linkTitle="BSPs and sensor data"
title = "Introduction to BSPs and sensor data"
weight = 20
pre = "› "
+++

Board support packages (BSPs) and libraries are two of the primary methods to interact and control any [microcontroller](https://en.wikipedia.org/wiki/Microcontroller) (MCU). A BSP is the software layer that contains hardware drivers and other routines you can use to access and run on-board hardware. 

The base routines are fully functional. They can be used as is or you can customize them to suit your use case. The BSP works with the toolchain and operating system to prepare the application to be uploaded and executed within the device. 

The {{< awsService type="edukit-short-en" >}} BSP sits on top of Espressif's IoT Developer Framework (ESP-IDF) and executes from the ESP32-D0WD MCU to all attached peripherals. You prepare an application to run on the {{< awsService type="edukit-short-en" >}} by using the BSP routines, the toolchain compiles the code into an executable format, and freeRTOS supplies the framework and logic for the MCU to execute the application. 

The {{< awsService type="edukit-short-en" >}} BSP is located in the project's `components/core2forAWS` directory and includes a file named `main.c` that acts as the primary executable.

#### Driver API libraries #### 

- *Microcontroller (Core2forAWS):* the main ESP32-D0WD MCU hardware helper APIs. For more information, see the {{< awsService type="docs-bsp-en" >}} guide: [Core2forAWS](https://edukit.workshop.aws/en/api-reference/core2foraws.html).

- *Accelerometer / gyroscope (MPU6886):* this library allows you access functions associated with the six-axis inertial measurement unit (IMU) and built-in temperature sensor. For more information, see the {{< awsService type="docs-bsp-en" >}} guide: [MPU6886]([(https://edukit.workshop.aws/en/api-reference/ili9342c.html). 

- *Side LEDs (SK6812):* the side LED bar helper libraries use the Adafruit NEOPIXEL library. For more information, see the {{< awsService type="docs-bsp-en" >}} guide: [SK6812](https://edukit.workshop.aws/en/api-reference/atecc608.html).

- *Display Controller (IlI9342C):* the display library provides functions that allow you to operate the display controller. For more information, see the {{< awsService type="docs-bsp-en" >}} guide: [Display](https://edukit.workshop.aws/en/api-reference/ili9342c.html).




#### Other libraries ###


- *C-SDK:*

- *cryptoauthlib:* (short sentence about it)
















---
{{% button href="https://github.com/aws-samples/aws-iot-edukit-tutorials/discussions" icon="far fa-question-circle" %}}Community support{{% /button %}} {{% button href="https://github.com/m5stack/Core2-for-AWS-IoT-EduKit/issues" icon="fas fa-bug" %}}Report bugs{{% /button %}}