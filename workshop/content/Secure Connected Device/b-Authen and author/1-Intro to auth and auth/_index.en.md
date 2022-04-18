+++
linkTitle="Introduction"
title = "Introduction to authentication and authorization"
weight = 10
pre = "› "
+++



### Introduction to transport layer security ###

Transport layer security (TLS) is a cryptographic protocol that is designed to provide communications security over a computer network. TLS ensures that application protocols remain confidential. TLS support is available in a number of programming languages and operating systems. 

For MQTT communication, TLS encrypts the connection between the device and the message broker. 


### X.509 certificates ###

X.509 is a standard that defines public key infrastructure where the public key is associated with an identity contained within a certificate. X.509 certificates can be issued by a trusted entity called a certificate authority (CA) or they can be self-signed. A CA maintains one or more special certificates called CA certificates that it uses to issue X.509 certificates. Only the CA has access to the private key of the CA certificate.

{{% notice info %}}
AWS requires a client certificate must be registered with AWS IoT before a client can communicate with AWS IoT. For more information, see AWS documentation: [X.509 client certificates](https://docs.aws.amazon.com/iot/latest/developerguide/x509-client-certs.html).
{{% /notice %}}



#### certificate chains ####


### TLS Handshake ###







---
{{% button href="https://github.com/aws-samples/aws-iot-edukit-tutorials/discussions" icon="far fa-question-circle" %}}Community support{{% /button %}} {{% button href="https://github.com/m5stack/Core2-for-AWS-IoT-EduKit/issues" icon="fas fa-bug" %}}Report bugs{{% /button %}}