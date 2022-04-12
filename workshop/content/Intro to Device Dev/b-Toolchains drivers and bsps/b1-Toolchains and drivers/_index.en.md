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


The {{< awsService type="edukit-long-en" >}} development kit consists of a development board, microcontroller (MCU), memory, input and output pins, and an interface for communication. In order to program, or provide instructions, to the {{< awsService type="edukit-short-en" >}} you must supply firmware. A toolchain consists of programming tools that help you develop and communicate firmware to your board. 

Toolchains can contain different tools, but commonly consist of a build system, cross compiler, board support packages (BSP), and software libraries. 
#### Build system ###

(CMake)



For more information, see [About CMake](https://cmake.org/overview/).



#### Cross compiler ###

(GCC)
A cross compiler translates the written code into executable code for the development board's processor. In our case, we're creating C programs and using the GNU Compiler Collection (GCC) 


For more information, see [GCC, the GNU Compiler Collection](https://gcc.gnu.org/) through GNU.org and [GNU Compiler Collection](https://en.wikipedia.org/wiki/GNU_Compiler_Collection) on Wikipedia. 

#### Board support packages ###


(BSP, or hardware drivers)


For more information, see [Core2 for AWS IoT EduKit BSP](https://edukit.workshop.aws/en/api-reference/index.html).


#### Software libraries ###


(IoT C-SDK) to create MCU applications


















___ 
{{% button href="https://github.com/aws-samples/aws-iot-edukit-tutorials/discussions" icon="far fa-question-circle" %}}Community support{{% /button %}} {{% button href="https://github.com/m5stack/Core2-for-AWS-IoT-EduKit/issues" icon="fas fa-bug" %}}Report bugs{{% /button %}}