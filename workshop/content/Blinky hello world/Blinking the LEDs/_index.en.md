+++
title = "Blinking the LEDs"
weight = 40
pre = "<b>d. </b>"
+++

Through the previous sections, you configured your device software, it's running, and you are connected to AWS IoT Core. Your AWS IoT EduKit is sending messages to the cloud, and is ready to receive and act on messages from the cloud. In this section, you subscribe to an [MQTT topic](https://docs.aws.amazon.com/iot/latest/developerguide/topics.html), view the messages that AWS IoT Core receives, and send an MQTT request to blink your device LEDs. 

MQTT is a [publish-subscribe protocol](https://mqtt.org/). This means that you can subscribe and publish to specific topics. The policy that the registration script created defines these topics. Your device can only send or receive messages to AWS IoT Core through the topics that satisfy the AWS IoT policy’s parameters and match the client ID ; in our case, the client ID is the same as the device’s secure element’s unique serial number. Understanding this process is critical so that you can filter messages and secure communication. 

## Subscribe through the AWS IoT MQTT client
The AWS IoT MQTT client in the AWS IoT Core console allows you to both view and publish MQTT messages. 

Complete the following steps to subscribe to an MQTT message topic:
1. Log into your AWS Account. 
1. Navigate to the [AWS IoT console](https://us-west-2.console.aws.amazon.com/iot/home?region=us-west-2#/) 
1. Choose **Test** in the navigation pane to open the client view.

{{< img "aws_iot-mqtt_test_client-subscribe.en.png" "Choose test in AWS IoT console" >}}

4. Confirm that the *Subscribe to a topic*` tab is active in the MQTT test client window.
1. Enter **#** (hash symbol) in theIn the Topic filter field to subscribe to *all* MQTT topic names. (The hash symbol, *#*, is a multi-level wild card [topic filter](https://docs.aws.amazon.com/iot/latest/developerguide/topics.html#topicfilters) and can only be used once and as the last character of a topic filter.)
1. Choose **Subscribe to topic**. 

The messages that your device sends to the cloud will begin to appear. (**Note:** this can take a minute or two before they appear) 

Because of the policy constraints, the device can only publish messages to the topic beginning with its client ID. This provides flexibility so that another subscriber (such as, a cloud application) to filter topics for specific devices. Filters can also be applied to display more specific topics; such as, a specific device's temperature readings. 

## Blink the LED
To start or stop the LED bars on the side of the AWS IoT EduKit from blinking, publish a message to the device from from the AWS IoT MQTT client in a topic that the device subscribes. The subscription topic for the device will have the pattern `<<CLIENT_ID>>/#`. You can view the subscription topic on the device after it successfully subscribes to the topic. Additionally, you can view the client ID that's been output on the host machine's serial monitor.

In the Publish box, enter the command below, after replacing the **<<CLIENT_ID>>** text with your actual client ID that you just copied. Then press the **Publish** button:
```
<<CLIENT_ID>>/blink
```
{{< img "aws_iot-mqtt_test_client-publish.en.png" "Subscribing to messages and publishing with AWS IoT console MQTT client" >}}
Your device should now have the side bar LEDs blinking. To pause the blinking, simply press the **Publish** button again to publish to the same topic.

{{% notice info %}}
To exit the serial monitor, press **CTRL** + **C**.
{{% /notice %}}

## Clean up
To optimize resources used and avoid unwanted possible AWS Cloud service charges, erase the flash on your device to get it ready for the subsequent tutorials. To erase the flash, you'll need to be in a project that has already been built (such as the one you just completed), exit a running serial monitor that might block the port (press **CTRL** + **C**), and use the command:

```
pio run --environment core2foraws --target erase
```


On to the final chapter, the [**conclusion**](conclusion.html).

---
{{% button href="https://github.com/aws-samples/aws-iot-edukit-tutorials/discussions" icon="far fa-question-circle" %}}Community support{{% /button %}} {{% button href="https://github.com/m5stack/Core2-for-AWS-IoT-EduKit/issues" icon="fas fa-bug" %}}Report bugs{{% /button %}}