+++
linkTitle="Toolchains and drivers"
title = "Overview of toolchains and drivers"
weight = 10
pre = "› "
+++

> Overview of toolchains and drivers
>    (short paragraphs: what is their function, why are they important)
>   * build systems (CMake)
>    * compilers (GCC)
>    * board support packages (BSP, aka hardware drivers)
>    * software libraries (IoT C-SDK) to create MCU applications
>    * How to research and find more information?
>    * VIDEO / ILLUSTRATION: demonstrating the parts working together
>    * (possible) CHECK IN: summarize key points in a quick review


___
> Developer boards consist of a microcontroller (MCU), memory (either integrated or add-on), input and output pins, and an interface for communication. ([IoT with PlatformIO](https://iotcon.de/blog/iot-konferenz/iot-with-platformio-part-one/) 
> In order to provide programming, or instructions, to the developer boards, you must supply firmware-smaller MCUs typically use C or C++ while more powerful boards will use Python and Javascript (also pulled from IoT with Platforms)
> The same applies to the tool chains of other manufacturers such as Particle or ARM Mbed OS. Usually you need the following parts if you want to develop in C or C++:
> * A crosscompiler capable of translating C/C++ code for the processor of the target hardware. In the open source area this is often the GCC, in a variant for the target. For example: arm-none-eabi-gcc for ARM Cortex processors/MCUs or xtensa-lx106-elf-gcc for the ESP series of Espressif.
> * The compiler includes additional tools such as linkers, preprocessors, archivers and others that work together to create an executable binary for the target hardware.
> * In most cases, a flashing tool is needed to get the firmware binary on the board – often via USB, in combination with a serial port, or via a programmer. Sometimes the USB interfaces of the boards allow you to access the board like a drive and copy the binary (or script for boards that support script languages) directly into a file system.<<>>


> Notes from: ([IoT with PlatformIO](https://iotcon.de/blog/iot-konferenz/iot-with-platformio-part-one/) 
___


> Toolchains, Espressif - ESP-IDF (IoT Development Framework) provides tools so that you can build firmware for your {< awsService type="edukit-short-en" >}}

___


Developer boards consist of a microcontroller (MCU), memory (either integrated or add-on), input and output pins, and an interface for communication. 

In order to provide programming, or instructions, to the developer boards, you must supply firmware. The toolchain consists of programming tools to help you develop and communicate the firmware to run your board. 



>   * Build systems (CMake)
>    * Cross compiler (GCC)
>    * Board support packages (BSP, aka hardware drivers)
>    * Software libraries (IoT C-SDK) to create MCU applications





>    * How to research and find more information?
>    * VIDEO / ILLUSTRATION: demonstrating the parts working together
>    * (possible) CHECK IN: summarize key points in a quick review






For more information, see [Core2 for AWS IoT Edukit BSP](https://edukit.workshop.aws/en/api-reference/index.html)


---
{{% button href="https://github.com/aws-samples/aws-iot-edukit-tutorials/discussions" icon="far fa-question-circle" %}}Community support{{% /button %}} {{% button href="https://github.com/m5stack/Core2-for-AWS-IoT-EduKit/issues" icon="fas fa-bug" %}}Report bugs{{% /button %}}