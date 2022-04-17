+++
linkTitle = "MQTT protocol" 
title = "MQTT protocol"
weight = 20
pre = "› "
+++


MQ Telemetry Transport (MQTT) is a lightweight and widely adopted messaging protocol that is commonly used within IoT applications because it is designed for constrained devices. The protocol communicates from machine to machine (M2M) by publishing to a topic and other devices that subscribe to that topic receive the information. For more information, see [MQTT.org](https://mqtt.org). 

### MQTT client and broker ###

An MQTT client is an device that runs an MQTT library and publishes and/or subscribes to an MQTT topic. An MQTT message broker, or server, receives all the messages, (optionally) filters them, and then sends the information to client(s) that subscribe to the specific topic. In our case, the {{< awsService type="edukit-short-en" >}} is the MQTT client that sends messages to {{< awsService type="iotcore-short-en" >}}, which acts as the message broker. Granted permission,  your device subscribes to topics and {{< awsService type="iotcore-short-en" >}} sends MQTT messages through these topics. For more information, see {{< awsService type="iotcore-short-en" >}} documentation: [Device communication protocols](https://docs.aws.amazon.com/iot/latest/developerguide/protocols.html).
### Topic names ###

The MQTT message broker uses topic names and topic filters to route messages from publishing clients to subscribing clients. MQTT topic names can represent a hierarchy of information by using the forward slash (/) character to separate the levels of the hierarchy. It is a best practice to keep topic names short and to embed a unique identifier or the client ID into the topic name; for example, '012345EXAMPLE1/blink'. For more information, see [Designing MQTT topics for AWS IoT Core](https://docs.aws.amazon.com/whitepapers/latest/designing-mqtt-topics-aws-iot-core/designing-mqtt-topics-aws-iot-core.html) and HiveMQ: [MQTT topics and best practices - MQTT essentials: part 5](https://www.hivemq.com/blog/mqtt-essentials-part-5-mqtt-topics-best-practices/)

{{% notice warning %}}
As you plan or subscribe to MQTT topic names, it is important to be aware of how you use the forward slash (/) character. Creating a topic name with a *leading forward slash* introduces an unnecessary topic level; for example, `/[clientID]/temperature`. Subscribing to a topic name with a *trailing forward slash* includes all child topic levels; for example, `[clientID]/sensor/` could include `[clientID]/sensor/temp` and `[clientID]/sensor/gyro`.
{{% /notice %}}

### Reserved topic names ###





> 
> `$aws/things/<<CLIENT_ID>>/shadow/update/accepted` 
> 








#### Wildcard topic filters ####

Publishing clients can't use wildcard characters in the topic names they publish. Wildcard characters are a form of filtering messages that the message broker will use for routing messages. 

* plus symbol (+): acts as a substitution for a *single level* within the topic.name; for example, subscribing to `[clientID]/sensor/+/room1`
  * receives messages from: `[clientID]/sensor/temp/room1` and `[clientID]/sensor/gyro/room1`
  * will not receive messages from: `[clientID]/sensor/temp/room2` or `[clientID]/sensor/gyro/room2`
* hash symbol (#): acts as a substitution for *multiple levels* within the topic; for example, subscribing to `[clientID]/sensor/#`
  * receives messages from: `[clientID]/sensor/temp/room1`, `[clientID]/sensor/gyro/room1`, `[clientID]/sensor/temp/room2`, and `[clientID]/sensor/gyro/room2`.
* trailing forward slash (/): acts the same as adding the hash symbol (#) at the end of a topic name.
### Limitations ###

There are a couple limitations that are important to know at this point:
* Topic length: the maximum topic length that the MQTT 5 specification defines is 65536 bytes, but the message broker may limit this size; for example, AWS IoT limits the length to 128.
* Packet size: the maximum message (or packet) size that the MQTT 5 specification defines is approximately 268 MB, but the message broker may limit this size; for example, AWS IoT limits the packet size to 128 kB.

For more information, see MQTT.org: [MQTT specifications](https://mqtt.org/mqtt-specification/)



### Subscribing to a topic ###



### Authenticating TLS using x.509 certificates ###





---
{{% button href="https://github.com/aws-samples/aws-iot-edukit-tutorials/discussions" icon="far fa-question-circle" %}}Community support{{% /button %}} {{% button href="https://github.com/m5stack/Core2-for-AWS-IoT-EduKit/issues" icon="fas fa-bug" %}}Report bugs{{% /button %}}