+++
linkTitle="Toolchains and drivers"
title = "Overview of toolchains and drivers"
weight = 10
pre = "› "
+++


> <<author note:>>

> IF WE'RE MOVING TO A WEB-BASED DEVELOPMENT ENVIRONMENT, WHY ARE WE TALKING ABOUT TOOLCHAINS AND THE ASSOCIATED SUPPORT PROGRAMS? I RECOGNIZE THA THEY ARE IMPORTANT AND ARE USED WITHIN OTHER / STANDARD DEVELOPMENT, BUT THIS WOULD MAKE MORE SENSE IF THE STUDENT WAS INSTALLING THESE APPLICATIONS.


> <<author note>>







The {{< awsService type="edukit-long-en" >}} development kit consists of a development board, microcontroller (MCU), memory, input and output pins, and an interface for communication. In order to program, or provide instructions, to the {{< awsService type="edukit-short-en" >}} you must supply firmware. A toolchain consists of programming tools that help you develop and communicate firmware to your board. 

Toolchains can contain different tools, but commonly consist of a build system, cross compiler, board support packages (BSP), and software libraries. 
#### Build system ###

A build system synchronizes the toolchain components, manages the build process, and helps to create the standard build files. We use [CMake]{https://cmake.org/} as our build system. For more information, see [About CMake](https://cmake.org/overview/).

#### Cross compiler ###

A compiler converts a program you supply into executable code that the platform can run. A cross compiler performs the same task and can compile code across multiple platforms. We use the GNU Compiler Collection (GCC ) as our cross compiler. For more information, see [GCC, the GNU Compiler Collection](https://gcc.gnu.org/) through GNU.org and [GNU Compiler Collection](https://en.wikipedia.org/wiki/GNU_Compiler_Collection) on Wikipedia. 

#### Board support packages ###

A board support package (BSP) is a collection of hardware-specific drivers and routines that allow a Real Time Operating System to function on a specific platform. For more information, see [Core2 for AWS IoT EduKit BSP](https://edukit.workshop.aws/en/api-reference/index.html).

#### Software libraries and software development kits ###

Software libraries are a collection of prewritten tools, templates, and code that provide functionality. They can also provide base code that can be customized to meet a specific need. Similarly, a software development kit (SDK) provides a software libraries that help to build platform-specific code or applications. Because much of the code that you flash to your {{< awsService type="edukit-short-en" >}} is in the C programming language, we utilize the AWS IoT C-SDK. For more information, see the [AWS IoT Device SDK for Embedded C](https://docs.aws.amazon.com/freertos/latest/userguide/c-sdk.html).



> << author note >>
> INSERT AN ILLUSTRATION THAT SHOWS HOW THESE COMPONENTS WORK TOGETHER
> 



> << author note >>
> POSSIBLE CHECK
> 






___ 
{{% button href="https://github.com/aws-samples/aws-iot-edukit-tutorials/discussions" icon="far fa-question-circle" %}}Community support{{% /button %}} {{% button href="https://github.com/m5stack/Core2-for-AWS-IoT-EduKit/issues" icon="fas fa-bug" %}}Report bugs{{% /button %}}