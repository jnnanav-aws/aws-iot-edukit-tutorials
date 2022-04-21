+++
title = "IoT policies"
weight = 20
pre = "› "
+++

As we discussed in the beginning of this lesson, authorization grants rights to access services and, potentially, perform tasks – consider this the *control* plane of authorization. Some users might have rights to update the firmware or change how often the {{< awsService type="edukit-short-en" >}} reports sensor information, while others cannot or have limited access. 

Another layer of authorization is the *data* plane, which is controlled by the IoT policy. IoT policies define the MQTT topics users and devices can use to publish or subscribe. By default, if a topic is not named in the policy, the user or device cannot publish or subscribe to that topic. In AWS IoT,  the data plane includes operations that allow you to connect to the AWS IoT Core message broker, send and receive MQTT messages, and get or update a thing's Device Shadow. For more information, see [AWS IoT Core policies](https://docs.aws.amazon.com/iot/latest/developerguide/iot-policies.html).




### IoT policies ###

IoT policies are [JSON](https://www.json.org/json-en.html) documents that allow you to define whether a device can publish or subscribe to a topic and which topics they can access. A single policy can be attached to multiple device certificates; therefore, you can attach a single policy across a fleet of devices. 

Each policy contains one or more policy statements, and each statement contains: 

- *Effect:* specifies whether the action is allowed or denied.
- *Action:* specifies the action the policy is allowing or denying.
- *Resource:* specifies the resource, or resources, that the action is allowed or denied access.

The following is part of a policy that was created during the [Blinky Hello World](../../../Blinky%20hello%20world/_index.en.md) tutorial: 

``` 
     {
      "Effect": "Allow",
      "Action": [
        "iot:Publish",
        "iot:Receive"
      ],
      "Resource": [
        "arn:aws:iot:us-east-2:111122223333:topic/myThingName/*",
        "arn:aws:iot:us-east-2:111122223333:topic/$aws/things/myThingName/shadow/*",
        "arn:aws:iot:us-east-2:111122223333:topic/$aws/things/myThingName/streams/*",
        "arn:aws:iot:us-east-2:111122223333:topic/$aws/things/myThingName/jobs/*"
      ]
     }
```





#### Wildcards and substitution variables ##
Wildcards and substitution variables may vary depending on the system that your {{< awsService type="edukit-short-en" >}} is registered. The following are a couple examples that are used within these tutorials and are allowed within AWS IoT. 
- asterisk symbol (*): represents one or more topic levels. 
  - For example, `arn:aws:iot:us-east-2:111122223333:topic/myThingName/*` would include `.../things/myThingName/temperatureData' and `.../things/myThingName/vibrationData'
- plus symbol (+): represents one topic level. 
  - for example,  `arn:aws:iot:us-east-2:111122223333:topic/myThingName/+/data` would include `.../myThingName/temperature/data` and `.../myThingName/vibration/data` but wouldn't include `.../myThingName/temperature/status`
- ${iot:Connection.Thing.ThingName}: confirms the device's thing name to the AWS IoT Core registry. If the device is registered within AWS IoT Core and the two names match, that policy action is able to be enacted. This is a convenient method to create a policy for multiple devices without having to know their device names ahead of time.



For more information, see [AWS IoT Core policy variables](https://docs.aws.amazon.com/iot/latest/developerguide/iot-policy-variables.html) and [Thing policy variables](https://docs.aws.amazon.com/iot/latest/developerguide/thing-policy-variables.html).










---
{{% button href="https://github.com/aws-samples/aws-iot-edukit-tutorials/discussions" icon="far fa-question-circle" %}}Community support{{% /button %}} {{% button href="https://github.com/m5stack/Core2-for-AWS-IoT-EduKit/issues" icon="fas fa-bug" %}}Report bugs{{% /button %}}