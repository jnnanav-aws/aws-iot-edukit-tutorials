+++
linkTitle="MCU system operations"
title = "Overview of MCU system operations"
weight = 10
pre = "› "
+++

> overview of mcu system operations
>     * Introduction
>         * Brief introduction to super-loops (synchronous execution of a single thread) and ISR (asynchronous interrupted execution of a separate thread)
>         * Asynchronous execution. Why is it important (internet and timing guarantees)
>     * Introduction to RTOS
>     * (possible) video/Illustration: show side-by-side comparison of running super loop versus rtos 


This tutorial uses [{{< otherService type="freertos-long-en" >}}](https://www.freertos.org/RTOS.html) as its operating system. Before we discuss the benefits of using {{< otherService type="freertos-short-en" >}} let's discuss a couple options for executing applications on an MCU. 

Many IoT devices execute their code in an endless loop. The following illustrates a some simple scenarios: 
- A device collects information from a temperature sensor and stores it onboard, sends it to a local storage device, or sends it to the cloud. This loop continues and the devices collects its data every minute. 
- A device actuates a motor to open and close a door. It waits for a signal to be sent from another device that has a movement sensor. When the movement sensor detects movement, it sends a signal to the device with the door actuator, which opens the door. The door actuator completes its cycle (opening and closing the door) and returns to the beginning of the loop while it waits for another signal. 




## Super loops ##





Execute their code in a *synchronous* format; meaning each task begins after the previous one ends. If the device is singly focused, such as collecting data from a temperature sensor, this may a perfect solution - the device runs its task in a loop and stores a temperature reading every minute. The device can be very small because it requires only enough resources to store the application, and a couple libraries to communicate with the sensor and store the data. 




#### When should you use a super loop ####











## Real-time operating systems ##

A real-time operating system (RTOS) executes applications *asynchronously* meaning that it will 


If there are several tasks involved in a device's process, however, each task must complete before the next task can begin. If the timing of the task is time sensitive, this could be a problem.






For more information, see the YouTube video series by Digi-Key and Shawn Hymel: [Introduction to RTOS](https://youtu.be/F321087yYy4).


#### When should you use an RTOS ####






> << author note: >>
> 
> insert illustration showing how synchronous and asynchronous 
> 
> operating systems might affect the time that
> 
> an application is executed. 







## {{< otherService type="freertos-short-en" >}} ##





#### When should you use {{< otherService type="freertos-short-en" >}}






---
{{% button href="https://github.com/aws-samples/aws-iot-edukit-tutorials/discussions" icon="far fa-question-circle" %}}Community support{{% /button %}} {{% button href="https://github.com/m5stack/Core2-for-AWS-IoT-EduKit/issues" icon="fas fa-bug" %}}Report bugs{{% /button %}}