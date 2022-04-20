+++
title = "IoT policies"
weight = 20
pre = "› "
+++


>  IoT policies
>     * Overview
>         * how does a policy support security
>     * brief description of the components / how to read a policy

> (possible) CHECK IN: summarize key points in a quick review

As we discussed in the beginning of this lesson, authorization grants rights to access services and, potentially, perform tasks –  consider this the *control* layer of authorization. Some users might have rights to update the firmware or change how often the {{< awsService type="edukit-short-en" >}} reports sensor information, while others cannot or have limited access. 

Another layer of authorization is the *data* layer, which is controlled by the IoT policy. IoT policies define the MQTT topics users and devices can use to publish or subscribe. By default, if a topic is not named in the policy, the user or device cannot publish or subscribe to that topic.

### IoT policy ##







#### Wildcards and substitution variables ##









---
{{% button href="https://github.com/aws-samples/aws-iot-edukit-tutorials/discussions" icon="far fa-question-circle" %}}Community support{{% /button %}} {{% button href="https://github.com/m5stack/Core2-for-AWS-IoT-EduKit/issues" icon="fas fa-bug" %}}Report bugs{{% /button %}}