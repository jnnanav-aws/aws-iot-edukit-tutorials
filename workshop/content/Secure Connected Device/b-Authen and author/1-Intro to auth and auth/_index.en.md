+++
linkTitle="Introduction"
title = "Introduction to authentication and authorization"
weight = 10
pre = "› "
+++

>  
> << author note >>
> you need an introductory sentence or two that ties these topics together
>  

### Introduction to transport layer security ###

Transport layer security (TLS) is a cryptographic protocol that is designed to provide communications security over a computer network. TLS ensures that application protocols remain confidential. TLS support is available in a number of programming languages and operating systems. For MQTT communication, TLS encrypts the connection between the device and the message broker. 

### X.509 certificates ###

X.509 is a standard that defines public key infrastructure where the public key is associated with an identity contained within a certificate. X.509 certificates can be issued by a trusted entity, called a certificate authority (CA), or they can be self-signed. A CA maintains one or more special certificates called CA certificates that it uses to issue X.509 certificates. Only the CA has access to the private key of the CA certificate.

One benefit of X.509 certificates, is that they enable devices to use asymmetric keys, which means that it utilizes a private key and a public key. X.509 certificates provide stronger client authentication over other schemes, such as user name and password or bearer tokens, because the private key never leaves the device. For more information, see [Using X.509 client certificates](https://docs.aws.amazon.com/iot/latest/developerguide/x509-client-certs.html).

You might consider this process similar to driving a car with a smart key system. You have a token (public key) that your car recognizes. As you approach the car, your key fob sends a public signal to the car, it authenticates you, and unlocks the car for you. If your battery became weak or you didn't want to transmit the signal, the key fob typically contains a physical key (private key) that you can use. 

{{% notice info %}}
AWS requires a client certificate must be registered with AWS IoT before a client can communicate with AWS IoT. For more information, see AWS documentation: [X.509 client certificates](https://docs.aws.amazon.com/iot/latest/developerguide/x509-client-certs.html).
{{% /notice %}}

Through out these tutorials, we use the X.509 certificate with a private and public key as our security solution. It is also worthwhile knowing a little about other security options such as X.509 certificate chains. 
#### certificate chains ####

An X.509 certificate chain is a list of certificates followed by a CA certificate. Typically, the first certificate in the chain begins with an end-entity certificate, which is a digitally-signed statement by the CA. The chain ends with a self-signed certificate, which is signed with the private key. In addition, the certificates in the chain have the following properties:

- The Issuer of each certificate (except the last one) matches the Subject of the next certificate in the list.
- Each certificate (except the last one) is signed by the secret key corresponding to the next certificate in the chain--this means that the signature of one certificate can be verified using the public key contained in the following certificate.
- The last certificate in the list is a trust anchor: a certificate that you trust because it was delivered to you by some trustworthy procedure.

For more information, see [Certificate chains and cross-certification](https://en.wikipedia.org/wiki/X.509#Certificate_chains_and_cross-certification).

### TLS Handshake ###

Transport layer security (TLS) is a protocol that allows for secure communication between a client and server and encrypts data during communication. 

During authentication, when both the client and server are being authenticated, they perform a TLS handshake, which means that the client and server exchange information and come to agreements on how they will communicate. For example, they may agree about which cipher suite (or algorithm) they will use to secure a TLS connection. After the handshake, the client and server have a successful TLS connection and can communicate. 

### Certificate best practices ###

When planning an IoT solution, it is important to incorporate the following certificate best practices: 

- Always give each device a unique certificate. This allows for fine-grained management of your devices. If an malicious user gains access to a single device, you want to be able to revoke the certificate for that particular unique device.
- Giving each device its own certificate also enables you to run checks to see if a certificate is shared by multiple devices. When multiple devices use the same certificate, this might indicate that a device has been compromised. Its identity then might have been cloned to further compromise the system.
- Devices must support rotation and replacement of certificates. This ensures smooth operation as certificates expire. 



For more information, see [Security best practices in {{< awsService type="iotcore-short-en" >}}](https://docs.aws.amazon.com/iot/latest/developerguide/security-best-practices.html).






---
{{% button href="https://github.com/aws-samples/aws-iot-edukit-tutorials/discussions" icon="far fa-question-circle" %}}Community support{{% /button %}} {{% button href="https://github.com/m5stack/Core2-for-AWS-IoT-EduKit/issues" icon="fas fa-bug" %}}Report bugs{{% /button %}}