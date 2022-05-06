+++
linkTitle="RTOS tasks"
title = "Introduction to RTOS tasks"
weight = 20
pre = "› "
+++
> {{< otherService type="freertos-short-en" >}}



RTOS applications can be structured as a set of tasks that run independently and do not rely on other tasks within the system. The RTOS scheduler is responsible to determine which task runs and in what order. Remember that the MCU is single threaded and runs only one task at a time. In order to accomplish running tasks asynchronously, the RTOS scheduler must start and stop each task several times as the application runs. Finally, the RTPS scheduler is responsible to ensure that the task is reinstated in the same state, or *context*, that it was when it was swapped. To achieve this each task is provided with its own stack. When the task is swapped out the execution context is saved to the stack of that task so it can also be exactly restored when the same task is later swapped back in.

## Task states

An RTOS task can exist in one of four states: 

- *Running*: When a task enters the Running state it is utilizing the processor. Again, because the processor is single threaded, there can be only one task in the Running state at a time.


- *Ready*: When a task is able to run and are not currently utilizing the processor, they are in a Ready state. Commonly, they are in this state because a task with a higher priority is currently in the Running state.



- *Blocked*: A task is Blocked if it cannot run because it is waiting for an event - a specific time (in the case of the temperature reading), an external input (in the case of the automatic door), or their turn in the queue. 
  - Blocked tasks have a *"timeout"* period, which gives them time for the event to occur. The task transitions to a Ready state after the timeout period whether the event has occurred or not. 
  - Tasks that are Blocked cannot not transition directly to a Running state - they must become Ready first.


- *Suspended*: Suspending a task is similar to blocking a task except that it doesn't have a timeout period. Tasks transition to and from the Suspended state through explicit API calls. 
  - Tasks that are Suspended cannot not transition directly to a Running state - they must become Ready first.

 




> <<Author note:>>
> create a simple diagram that mirrors the one in the freertos documentation https://www.freertos.org/RTOS-task-states.html







## Task controls


> FROM RASHED: 
> For task control, we should cover the following:
> •	xTaskCreatePinnedToCore this is a modified version of the vanilla FreeRTOS xTaskCreate which accepts an additional argument since the ESP32 is dual core.
> •	vTaskSuspend
> •	vTaskDelay
> •	vTaskResume
> •	vTaskDelete

> For task communications the two below is sufficient for someone starting off, a nice to have is xTaskNotify if we can squeeze that in since that’s a newer more performant way of communicating simple things among tasks:
> •	Queues
> •	Semaphores/Mutexes




## Inter-task communication and task synchronization




> <<author note:>>
> https://www.embedded.com/inter-task-communication-and-synchronization/


>  RTOS inter-task communication and task synchronization 
>     (short paragraphs: what is their function, why are they important)
>     * Queues
>     * Mutexes / Semaphores
>     * Event Groups
>     * (possible) CHECK IN: summarize key points in a quick review
















For more information, see FreeRTOS: [Tasks and co-routines](https://www.freertos.org/taskandcr.html).



---
{{% button href="https://github.com/aws-samples/aws-iot-edukit-tutorials/discussions" icon="far fa-question-circle" %}}Community support{{% /button %}} {{% button href="https://github.com/m5stack/Core2-for-AWS-IoT-EduKit/issues" icon="fas fa-bug" %}}Report bugs{{% /button %}}