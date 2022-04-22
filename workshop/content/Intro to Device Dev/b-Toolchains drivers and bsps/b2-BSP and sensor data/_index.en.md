+++
linkTitle="BSPs and sensor data"
title = "Introduction to BSPs and sensor data"
weight = 20
pre = "› "
+++

>
> SPEND SOME TIME with the introduction to bsps and libraries 
>
>     * Introduction to BSPs and libraries
>         * highlight EduKit’s “top 5” BSP API’s and their respective API reference 
>         * Other libraries that are included in project template
>             * C-SDK
>             * cryptoauthlib (short sentence about it)
>     * (possible) CHECK IN: summarize key points in a quick review

Board support packages (BSPs) and application programming interface (API) libraries are two of the primary methods to interact and control any [microcontroller](https://en.wikipedia.org/wiki/Microcontroller) (MCU). A BSP is the software layer that contains hardware drivers and other routines you can use to access and run on-board hardware. 

The included routines are fully functional. They can be used as is or customized to suit your use case. The BSP works with the toolchain and operating system (in our case, freeRTOS) to prepare the application to be uploaded and executed within the device. 

The {{< awsService type="edukit-short-en" >}} BSP sits on top of Espressif's IoT Developer Framework (ESP-IDF) and executes from the ESP32-D0WD MCU to all attached peripherals. You prepare an application to run on the {{< awsService type="edukit-short-en" >}} by using the BSP routines, the toolchain compiles the code into an executable format, and freeRTOS supplies the framework and logic for the MCU to execute the application. 

The {{< awsService type="edukit-short-en" >}} BSP is located in the project's `components/core2forAWS` directory and includes a file named `main.c` that acts as the primary executable.

#### Driver APIs #### 




















---
{{% button href="https://github.com/aws-samples/aws-iot-edukit-tutorials/discussions" icon="far fa-question-circle" %}}Community support{{% /button %}} {{% button href="https://github.com/m5stack/Core2-for-AWS-IoT-EduKit/issues" icon="fas fa-bug" %}}Report bugs{{% /button %}}