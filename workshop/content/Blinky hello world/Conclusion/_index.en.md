+++
title = "Conclusion"
weight = 50
pre = "<b>e. </b>"
+++

Hopefully you enjoyed the journey of building your cloud connected blinky project. Using PlatformIO, you were able to configure, build, flash, and monitor your Core2 for {{<awsEdukitShort-en>}}'s firmware. Your device is now registered as an AWS IoT thing in your AWS account for secure cloud connectivity using on-board secure hardware. You connected to AWS IoT Core, sent messages from the device over MQTT, and received an MQTT message from the AWS IoT console's MQTT client which was used to toggle the lights on the device.

While the {{<awsEdukitShort-en>}} program does not teach C or require it, it is critical for embedded development. The control and flexibility from the lower level code allows you to gain the maximum potential from your hardware. If you are not familiar with C programming but curious to learn or if you are a bit rusty and want dive into the application code we provide in this program, Jens Gustedt provides [Modern C](https://modernc.gforge.inria.fr/) under the Creative Commons license and it is free to [download](https://modernc.gforge.inria.fr/download.html). 

## What's Happening on the Device
## The FreeRTOS Kernel
The application on the device runs using the [FreeRTOS kernel](https://www.freertos.org/)—[a real-time operating system](https://www.freertos.org/about-RTOS.html) (RTOS). It is bundled into the binary you compiled (as well as other libraries and drivers) with your application code. The FreeRTOS kernel schedules a block of sequential code as a [task](https://www.freertos.org/taskandcr.html) to give it a share of processor run time. There are tasks that typically loop forever to create messages to be sent to AWS, process received messages, update the display, blink the LEDs, etc. 

The Core2 for {{<awsEdukitShort-en>}} packs a 240MHz dual core processor, however, it pales in comparison to the 8+ core at 4+GHz computers common today. To make the most out of the precious processor time, the FreeRTOS kernel puts [tasks in a states](https://www.freertos.org/RTOS-task-states.html) such as running or suspended. The FreeRTOS kernel gives microcontroller applications the ability to optimize the processor by rapidly switching between individual tasks. A task can run once another task has put itself into a suspended or blocked state (see diagram below). This gives the appearance of concurrency and greatly improves an embedded application's performance when compared to a simpler [super loop application](https://en.wikibooks.org/wiki/Embedded_Systems/Super_Loop_Architecture). 
{{< img "RTOS_scheduling_execution.en.png" "Example of FreeRTOS application scheduling" "1 - MQTT starts running, 2 - MQTT blocked (no new messages) & display starts running, 3 - MQTT running, processing message & display blocked, 4 - MQTT blocked & blink task running (LED on), 5 - Blink blocked & display running, 6 - Display blocked & blink running (LED off), 7 - Blink blocked & display running">}}

While super loop applications are simpler to program, areas of code that block/delay execution of other code cause the MCU to sit idle. A device connecting to the AWS cloud will have variable round-trip latency and bandwidth constraints that make the performance advantage of using an RTOS necessary. An RTOS provides significant advantages for other applications where it's paramount to not lose data or to be able to perform a critical operation without being obstructed by another code block's execution (e.g. health and safety), or to simply drive a smooth display screen.
{{< img "super_loop_execution.en.png" "Example of super loop application execution" "1 - MQTT message interrupt starts, 2 - MQTT message processing finished & LED toggles on, code execution pauses for 500ms, LED toggles off, pauses execution for 500ms, 3 - End of blink code & start of display refresh, 4 - End of Display code & LED toggles on, pauses execution for 500ms, LED off, pauses execution for 500ms" >}}

To learn more about RTOS' and FreeRTOS, view [this video series](https://www.youtube.com/watch?v=F321087yYy4) and visit [FreeRTOS.org](https://www.freertos.org/RTOS.html).

## AWS IoT Device SDK for Embedded C
The [AWS IoT Device SDK for Embedded C](https://github.com/espressif/aws-iot-device-sdk-embedded-C/tree/61f25f34712b1513bf1cb94771620e9b2b001970) used in this example provided simplified connectivity and messaging to/from AWS IoT and was able to work with the included secure element library to make device authentication easy. The Device SDK for Embedded C is located in the `Core2-for-AWS-IoT-EduKit/Blink-Hello-World/components/esp-aws-iot/` folder.

## The Board Support Package — Device Drivers
The device's hardware features such as the screen, power management chip, secure element, speaker, microphone, 6-axis [inertial measurement unit](https://en.wikipedia.org/wiki/Inertial_measurement_unit) (IMU), touch driver, LED bar, and more are bundled as a board support package (BSP). The BSP are drivers with APIs that provides a simplified way to accessing the features of the hardware. The BSP is located in the `Core2-for-AWS-IoT-EduKit/Blink-Hello-World/components/core2foraws/` folder. In this example, the SK6812 driver was used to control the side LED bars and the [LVGL library](https://docs.lvgl.io/v7/en/html/) was used to show the elements on the display. To view the available application programming interfaces (APIs) of the BSP and their usage, see the <a href="https://edukit.workshop.aws/en/api-reference/index.html" target="_blank">Core2 for {{<awsEdukitShort-en>}} API reference</a>.

On to the next tutorial, [**Smart Thermostat**](/en/smart-thermostat.html).

---
{{% button href="https://github.com/aws-samples/aws-iot-edukit-tutorials/discussions" icon="far fa-question-circle" %}}Community support{{% /button %}} {{% button href="https://github.com/m5stack/Core2-for-AWS-IoT-EduKit/issues" icon="fas fa-bug" %}}Report bugs{{% /button %}}