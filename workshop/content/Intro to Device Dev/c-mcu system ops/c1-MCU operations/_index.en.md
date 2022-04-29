+++
linkTitle="MCU system operations"
title = "Overview of MCU system operations"
weight = 10
pre = "› "
+++

It is common that IoT devices run in an endless loop. To illustrate this, consider the following scenarios: 
- Collecting temperature data: a device collects information from a temperature sensor every minute and stores it (possibly saving it onboard, sending it to a local storage device, or sending it to the cloud). This loop continues and the device continuously collects and stores readings. 
- Motion activated door: a device with a motion sensor checks every second to determine movement. When it senses movement, it sends a signal to an actuator that opens a door. The door opens and closes. Afterward, the code returns to the beginning of the loop, the motion sensor continues to check for movement, and the actuator checks for a signal to open the door. 
- Parking spot indicator: a sensor checks every 30 seconds to see if there is a vehicle parked underneath it. When the sensor reading is `FALSE` (meaning, no car), it sets an indication light to green. When the sensor reading is `TRUE` (meaning, a car is present), it sets an indication light to red. The sensor continuously checks and indicates the parking spot's status through the lights that it controls. 

Many IoT devices contain a small MCU so that they can fit within a desired form factor. Because of their size, they are resource constrained, run their code in a loop, and process one task at a time.

## Super loops

Super loops run their code in a *synchronous* format; meaning that each task begins after the previous one ends. If the device is singly focused, such as collecting data from a temperature sensor, this may a perfect solution - the device runs its task in a loop and stores a temperature reading every prescribed interval. This device can be very small because it requires only enough resources to store and run the application. It will also need a couple libraries so that it can communicate with the sensor and store the data. 

This approach to running an IoT device is common and effective for many applications. The super loop typically requires low memory and CPU consumption, it's easy to write and debug, and you can set it to wait for a specific amount of time or a signal before running its tasks. 



> <<author note:>>
> insert an illustration demonstrating tasks running in a super loop and, possibly, a time table of how their task might run. 



The super loop is ideal for situations where you have one or more tasks that can be processed in order and their exact timing is not imperative. On the other hand, if one of the tasks takes longer than normal to process or is waiting for an input, the following tasks will not run until the current task completes. If there is a critical task that must execute at a specific time or should take priority, such as in a medical scenario, the super loop is not the best solution. 



> <<author note:>>
> insert an illustration demonstrating tasks running in a super loop and one becomes delayed. include a time table of how their task might run. 



## Real-time operating systems 

A real-time operating system (RTOS) can run tasks *asynchronously* and the tasks can be assigned a priority. An RTOS will not change the capabilities of the MCU. A single-threaded MCU is still a single-threaded MCU regardless of what software architecture it uses. To achieve *asynchronous* processing, the operating system runs multiple tasks and *shares* the processor;  therefore, if three tasks share CPU time, each one will run for very short periods until they complete. 



> <<author note:>>
> insert an illustration demonstrating tasks sharing CPU time and, possibly, a time table of how their task might run. 



In addition, to running sharing processing time, an ROTS allows you to assign a priority to a task; therefore, if a task is waiting for input or taking longer than normal to process, a higher priority task can be processed. As well, if a task is running and a higher priority task needs to be processed, the RTOS will save the lower priority's state to allow the higher priority task to complete. Once the higher priority task completes, the operating system restores the lower priority task. This process is called *context switching*. 


> <<author note:>>
> insert an illustration demonstrating tasks sharing CPU time and a higher priority task is inserted and processed. possibly, a time table of how their task might run. 

Because an RTOS can run tasks asynchronously and based on priority, it is more efficient and consistent than a super loop. For more information, see the YouTube video series by Digi-Key and Shawn Hymel: [Introduction to RTOS](https://youtu.be/F321087yYy4) and [ROTS Fundamentals](https://www.freertos.org/implementation/a00002.html).



### {{< otherService type="freertos-long-en" >}}

Many of the {{< awsService type="edukit-short-en" >}} tutorials use [{{< otherService type="freertos-short-en" >}}](https://www.freertos.org/RTOS.html). {{< otherService type="freertos-short-en" >}} is a class of RTOS that is designed to be small enough to run on a microcontroller - although its use is not limited to microcontroller applications. 

{{< otherService type="freertos-short-en" >}} is distributed through an open source, MIT license that does not require you to expose your proprietary IP. We find {{< otherService type="freertos-short-en" >}} to be reliable, feature rich, and scalable. It includes a multitasking scheduler, memory allocation, intertask coordination, and support for symmetric multiprocessing (SMP) on a multi-core microcontroller. Finally, {{< otherService type="freertos-short-en" >}} includes libraries that enhance connectivity, security, and over-the-air (OTA) updates. 

For more information, see [What is FreeRTOS?](https://docs.aws.amazon.com/freertos/latest/userguide/what-is-freertos.html) and [Why FreeRTOS?](https://freertos.org).





---
{{% button href="https://github.com/aws-samples/aws-iot-edukit-tutorials/discussions" icon="far fa-question-circle" %}}Community support{{% /button %}} {{% button href="https://github.com/m5stack/Core2-for-AWS-IoT-EduKit/issues" icon="fas fa-bug" %}}Report bugs{{% /button %}}