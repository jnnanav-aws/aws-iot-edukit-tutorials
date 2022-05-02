+++
title = "Secure Connected Device"
chapter = true
weight = 92
pre = "<b>12. </b>"
+++


This tutorial presents introductory information about securing your device. Security is an essential concern for any interaction through the Internet - more so with Internet of Things (IoT) devices. Because IoT devices are resource constrained, it is common that *bad actors* try to take advantage of them. 

We begin this tutorial by discussing how to communicate with and receive information from your {{< awsService type="edukit-short-en" >}} using MQ Telemetry Transport (MQTT). This provides a secure method to check your device's status, update its application, and receive information and data. 

In addition, it is imperative that your device verifies (authenticates) all communications and connections. The {{< awsService type="edukit-short-en" >}} uses secure X.509 certificates and other security strategies that we discuss later in this tutorial. 


To begin, continue to [**Controlling peripherals through MQTT**](secure-connected-device/a-intro-to-mqtt.html).

 

---
{{% button href="https://github.com/aws-samples/aws-iot-edukit-tutorials/discussions" icon="far fa-question-circle" %}}Community support{{% /button %}} {{% button href="https://github.com/m5stack/Core2-for-AWS-IoT-EduKit/issues" icon="fas fa-bug" %}}Report bugs{{% /button %}}