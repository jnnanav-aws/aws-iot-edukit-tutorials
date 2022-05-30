+++
linkTitle="RTOS tasks"
title = "Introduction to RTOS tasks"
weight = 20
pre = "› "
+++

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

Task controls allow you to affect the behavior for how your task processes. The following outlines some common task controls: 


- `xTaskCreate` creates a new task and adds it to the list of tasks that are in a *Ready* state. The following provides an example of this control: 

```
void vAFunction( void )
 {
 TaskHandle_t xHandle;

     // Create a task, storing the handle.
     xTaskCreate( vTaskCode, "NAME", STACK_SIZE, NULL, tskIDLE_PRIORITY, &xHandle );

...
}
```





- `xTaskCreatePinnedToCore` is similar to `xTaskCreate` and is extended so that it can be used with a MCU with multiple cores. For example, the {{< awsService type="edukit-short-en" >}} is a dual processor. This control creates a new task, adds it to the list of tasks that are in a *Ready* state, and specifies which core should process it. 


```
void vAFunction( void )
 {
 TaskHandle_t xHandle;

     // Create a task, storing the handle.
     xTaskCreatePinnedToCore( vTaskCode, "NAME", STACK_SIZE, NULL, tskIDLE_PRIORITY, 0, &xHandle );

     // ...
}
```


- `vTaskDelay` changes the task's status to *Blocked* for a specific number of ticks. The amount of time  that `vTaskDelay` affects a task depends on the MCU tick rate. 

   *Caution – over simplification:* One tick equals one MCU cycle. For example, a 1 hz MCU processes on cycle, or 1 tick, per second. As well, a 1 Mhz single core processor, processes 1,000,000 cycles per second. 

   `portTICK_RATE_MS` parameter: Because the chronological value of a tick varies based on the MCU that's processing the task, this parameter converts the tick into a predictable measurement – milliseconds. 

   The following provides an example of this control from the [Smart Thermostat](https://edukit.workshop.aws/en/smart-thermostat/data-acquisition.html) tutorial: 


```
{
  {
    // ...
  for (;;) {
    MPU6886_GetTempData(&temperature);
    temperature = (temperature * 1.8)  + 32 - 50;
    ESP_LOGI("thermostat", "measured temperature is: %f", temperature);

    // sleep for 1000ms before continuing the loop
    vTaskDelay(1000 / portTICK_RATE_MS);
  }
}
```




- `vTaskDelete` removes a task from the RTOS kernels management; including all *Ready*, *Blocked*, *Suspended*, and event lists. The following provides an example of this control: 

```
 void vOtherFunction( void )
 {
 TaskHandle_t xHandle = NULL;

     // Create the task, storing the handle.
     xTaskCreate( vTaskCode, "NAME", STACK_SIZE, NULL, tskIDLE_PRIORITY, &xHandle );

     // Use the handle to delete the task.
     if( xHandle != NULL )
     {
         vTaskDelete( xHandle );
     }
 }
```







- `vTaskSuspend` places a task into the *Suspended* state. The following provides an example of this control *(note: `vTaskResume` extends this example to show how a task can be suspended and then resumed)*:

```
void vAFunction( void )
 {
 TaskHandle_t xHandle;

     // Create a task, storing the handle.
     xTaskCreate( vTaskCode, "NAME", STACK_SIZE, NULL, tskIDLE_PRIORITY, &xHandle );

     // ...

     // Use the handle to suspend the created task.
     vTaskSuspend( xHandle );

     // ...


 }
```








- `vTaskResume` resumes a suspended task by placing it into the *Ready* state. The following provides an example of this control:

```
void vAFunction( void )
 {
 TaskHandle_t xHandle;

     // Create a task, storing the handle.
     xTaskCreate( vTaskCode, "NAME", STACK_SIZE, NULL, tskIDLE_PRIORITY, &xHandle );

     // ...

     // Use the handle to suspend the created task.
     vTaskSuspend( xHandle );

     // ...

     // The created task will not run during this period, unless
     // another task calls vTaskResume( xHandle ).

     //...

     // Resume the suspended task ourselves.
     vTaskResume( xHandle );

     // The created task will once again get microcontroller processing
     // time in accordance with its priority within the system.
 }
```






For more information, see FreeRTOS: [API Reference, Task Control](https://www.freertos.org/a00112.html). 


## Inter-task communication and task synchronization

> Author note: TO BE WRITTEN (WIP)
> 





> <<author note:>>
> https://www.embedded.com/inter-task-communication-and-synchronization/

> For task communications the two below is sufficient for someone starting off, a nice to have is xTaskNotify if we can squeeze that in since that’s a newer more performant way of communicating simple things among tasks:
> •	Queues
> •	Semaphores/Mutexes



>  RTOS inter-task communication and task synchronization 
>     (short paragraphs: what is their function, why are they important)
>     * Queues
>     * Mutexes / Semaphores
>     * Event Groups


- *Queues* are the primary method that tasks communicate between each other. Queues can also be used to communicate between interrupts and tasks. In most cases they are used as thread safe buffer that operates with a *first in first out* (FIFO) strategy - meaning that new data is sent to the back of the queue by default.


>     * (possible) CHECK IN: summarize key points in a quick review
















For more information, see FreeRTOS: [Queues, Mutexes, and Semaphores](https://www.freertos.org/Embedded-RTOS-Queues.html) and [Tasks and co-routines](https://www.freertos.org/taskandcr.html)



---
{{% button href="https://github.com/aws-samples/aws-iot-edukit-tutorials/discussions" icon="far fa-question-circle" %}}Community support{{% /button %}} {{% button href="https://github.com/m5stack/Core2-for-AWS-IoT-EduKit/issues" icon="fas fa-bug" %}}Report bugs{{% /button %}}