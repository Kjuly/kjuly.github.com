---
layout: post
title: "iOS APNs: Installing the SSL Certificate and Key on the Server"
date: 2012-04-26 01:09
comments: true
categories: 
- iOS
- Security
---

You should install the SSL distribution certificate and private cryptographic key you obtained earlier on the server computer on which the provider code runs and from which it connects with the sandbox or production versions of APNs (Apple Push Notifications). To do so, complete the following steps:

1. Open Keychain Access utility and click the `My Certificates` category in the left pane.

2. Find the certificate you want to install and disclose its contents.
You'll see both a certificate and a private key.

3. Select both the certificate and key, choose `File` > `Export Items`, and export them as a `Personal Information Exchange (.p12)` file.

4. Servers implemented in languages such as Ruby and Perl often are better able to deal with certificates in the Personal Information Exchange format. To convert the certificate to this format, complete the following steps:
    1. In KeyChain Access, select the certificate and choose `File` > `Export Items`. Select the Personal Information Exchange (.p12) option, select a save location, and click Save.
    2. Launch the Terminal application and enter the following command after the prompt:

            openssl pkcs12 -in CertificateName.p12 -out CertificateName.pem -nodes

5. Copy the `.pem` certificate to the new computer and install it in the appropriate place.

Tip: generally, the `.pem` should be put to `~/.ssh/` as a private key.


### Reference:

[Local and Push Notification Programming Guide][]

[Local and Push Notification Programming Guide]: http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ProvisioningDevelopment/ProvisioningDevelopment.html
