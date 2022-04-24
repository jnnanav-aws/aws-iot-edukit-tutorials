+++
linkTitle="BSPs and sensor data"
title = "Introduction to BSPs and sensor data"
weight = 20
pre = "› "
+++

Board support packages (BSPs) and libraries are two of the primary methods to interact and control any [microcontroller](https://en.wikipedia.org/wiki/Microcontroller) (MCU). A BSP is the software layer that contains hardware drivers and other routines you can use to access and run on-board hardware. Your applications use BSP application programming interfaces (APIs) to collect data locally or send data to a server. You can also use BSP APIs to control hardware and peripherals that are attached to the MCU, 

Base BSP routines are fully functional. They can be used as is or you can customize them to suit your use case. The BSP also works with the toolchain and operating system to prepare the application to be uploaded and executed within the device. 

The {{< awsService type="edukit-short-en" >}} BSP sits on top of Espressif's IoT Developer Framework (ESP-IDF) and executes from the ESP32-D0WD MCU to all attached peripherals. You prepare an application to run on the {{< awsService type="edukit-short-en" >}} by using the BSP routines, the toolchain compiles the code into an executable format, and freeRTOS supplies the framework and logic for the MCU to execute the application. 

The {{< awsService type="edukit-short-en" >}} BSP is located in the project's `components/core2forAWS` directory and includes a file named `main.c` that acts as the primary executable file.

#### Driver API libraries #### 

The following highlights a few of the BSP API libraries that you will commonly use: 

- *Microcontroller (Core2forAWS):* this is the main main library for the  the {{< awsService type="edukit-short-en" >}}. This library includes the ESP32-D0WD MCU hardware helper functions that enable basic hardware features. They initialize and configure the hardware with preset parameters. For more information, see the {{< awsService type="docs-bsp-en" >}} guide: [Core2forAWS](https://edukit.workshop.aws/en/api-reference/core2foraws.html).

- *Accelerometer / gyroscope (MPU6886):* this library allows you access functions associated with the six-axis inertial measurement unit (IMU) and built-in temperature sensor. For more information, see the {{< awsService type="docs-bsp-en" >}} guide: [MPU6886]([(https://edukit.workshop.aws/en/api-reference/ili9342c.html). 

- *Side LEDs (SK6812):* the side LED bar helper libraries use the Adafruit NEOPIXEL library. For more information, see the {{< awsService type="docs-bsp-en" >}} guide: [SK6812](https://edukit.workshop.aws/en/api-reference/atecc608.html).

- *Display Controller (IlI9342C):* the display library provides functions that allow you to operate the display controller. For more information, see the {{< awsService type="docs-bsp-en" >}} guide: [Display](https://edukit.workshop.aws/en/api-reference/ili9342c.html).

#### Other libraries ###


- ESP-AWS-IoT: the library works with the AWS IoT Device Embedded SDK and enables AWS IoT cloud connectivity for the {{< awsService type="edukit-short-en" >}}. It is a collection of C source files under the MIT open source license that can be used in embedded applications to securely connect IoT devices to AWS IoT Core. For more information, see the Espressif repository on GitHub: [esp-aws-iot](https://github.com/espressif/esp-aws-iot) and the AWS repository on GitHub: [aws-iot-device-skd-embedded-C](https://github.com/aws/aws-iot-device-sdk-embedded-C/find/main).


- *esp-cryptoauthlib:* The library is a part of Microchip's cryptoauthlib for ESP-IDF, which is a support library that specializes in securing small processors. It supports X.509 certificates and TLS integration. It also contains necessary build support to use cryptoauthlib with ESP-IDF. For more information, see the Espressif repository on GitHub: [Core2-for-AWS-IoT-EduKit](https://github.com/m5stack/Core2-for-AWS-IoT-EduKit/tree/master/Blinky-Hello-World/components/esp-cryptoauthlib) and [Mircorchip CryptoAuthLib](https://www.microchip.com/en-us/software-library/cryptoauthlib).


---
{{% button href="https://github.com/aws-samples/aws-iot-edukit-tutorials/discussions" icon="far fa-question-circle" %}}Community support{{% /button %}} {{% button href="https://github.com/m5stack/Core2-for-AWS-IoT-EduKit/issues" icon="fas fa-bug" %}}Report bugs{{% /button %}}