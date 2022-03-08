+++
linkTitle = "Windows"
title = "Windows 10 Set Up Instructions"
pre = "› "
+++

This section provides information to configure your Windows computer (host machine) to download, view, and edit code from the AWS IoT EduKit GitHub repository. When you complete these steps, your computer will be ready to compile and upload code to the hardware's flash memory. Finally, these steps are required to install the ESP RainMaker agent.

## Install Git and Git dependencies
To download the code from the remote code repository on GitHub, you need to install [Git](https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F), which is a widely adopted distributed version control system. Git is commonly used for source code management and collaboration. Git also allows users to track file changes, and distribute code between a local machine and remote server (for more information, see [About Git](https://git-scm.com/about)). 

Complete the following steps to install OpenSSL, Git, and Git's dependencies:
1. Download and install [OpenSSL](https://www.openssl.org/source/).
1. Download and install [Git for Windows](https://git-scm.com/download/win).
   * When you install Git for Windows, use the default options and be sure to choose **Use the OpenSSL library** in the *Choosing HTTPS transport backend installer* page.

![Git for Windows installation wizard. Choose Use the OpenSSL library](windows/git-for-windows-openssl2.png?width=450px&classes=shadow)

## Set up Silicon Labs USB-to-UART bridge
The AWS IoT EduKit communicates with the host machine through a Silicon Labs CP210x USB-to-UART bridge. The on-board CP2104 is an USB-to-UART bridge that facilitates host communication with the ESP32-D0WD microcontroller. The microcontroller communicates bi-directionally over [UART](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-reference/peripherals/uart.html)0, which the CP210x translates through a virtual communication port on the host machine it establishes over USB-C. To be able to mount the virtual serial port and communicate across it, you must download and install the corresponding driver.
1) Ensure the AWS IoT EduKit device is not connected to host machine.
2) Download the [Windows Silicon Labs CP210x](https://www.silabs.com/documents/public/software/CP210x_Universal_Windows_Driver.zip) driver.
3) Extract the downloaded file.
   {{% notice info %}}
   You must extract the contents of the folder. The driver will not install if the executable runs within the archive. Also, where you save the extracted file is not important. 
   {{% /notice %}} 
4) Run the **CP210xVCPInstaller_x64.exe** installer.
5) Restart your host machine now to make sure the driver is applied.

## Install Visual Studio Code
Visual Studio Code (VS Code) is an open source integrated development environment (IDE) that allows you to view, edit, and manage code. Download the latest [VS Code](https://code.visualstudio.com/) software for your operating system. To troubleshoot issues with Visual Studio Code's installation or use, refer to [Setting up Visual Studio Code](https://code.visualstudio.com/docs/setup/setup-overview) in their documentation.

## Install PlatformIO
[PlatformIO](https://marketplace.visualstudio.com/items?itemName=platformio.platformio-ide) (PIO) provides a professional embedded development platform that simplifies embedded software development. This Visual Studio Code extension combines the functionality of the Platform IO command line interface (CLI) with a graphical user interface (GUI). For more information about PIO and directions to download and install the extension, see [PlatformIO's installation instructions](https://platformio.org/install/ide?install=vscode).

Restart VS Code after the PlatformIO extension installation completes.

## Clone the code repository
All of the projects and files exist in a [GitHub repository](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/about-repositories), where you can also view the revision history of each file in the repository (repo). To clone the code for the tutorials, you'll use the PIO interface:
1) Choose the **PlatformIO logo** on the VS Code activity bar (left most menu).
2) From PlatformIO's **Quick Access** menu, expand **Miscellaneous**, and select **Clone Git Project**.
3) Paste `https://github.com/m5stack/Core2-for-AWS-IoT-EduKit.git` into the text field and select the location that you want to save the project.
{{< img "pio-clone_git_project.en.png" "PlatformIO Clone Git Project" "1 - Open PIO menu, 2 - Clone git project, and 3 - Paste repository URL" >}}

## Download and install the phone apps
The ESP RainMaker Phone Apps are available for iOS and Android phones to provide Wi-Fi network configuration, user-creation, user-device association, and device control. The apps can be found through the following locations:
* Android: [Google PlayStore](https://play.google.com/store/apps/details?id=com.espressif.rainmaker), [Direct APK](https://github.com/espressif/esp-rainmaker-android/releases)
* iOS: [Apple App Store](https://apps.apple.com/app/esp-rainmaker/id1497491540)

If you don't have a compatible Android or iOS device, you can follow the [ESP RainMaker CLI Setup](https://rainmaker.espressif.com/docs/cli-setup.html) instructions.

## Identify the device communication port
If you haven't already, unbox the AWS IoT EduKit and connect it to your host computer's USB 2.0 port using the supplied USB-A to USB-C cable. (You do not need to use the hex key that is included. This key is used to install additional modules that are sold separately.) 

The device should automatically turn on when you plug it in. If it doesn't, press the power button.
![How to turn M5Stack Core2 for AWS on or off](windows/core2foraws_power_on_off.jpg?width=500px&classes=shadow)

Now that the device is ready and the prerequisite software is installed, let's identify the virtual port your device is using so that you can correctly route read and write operations.

1) From PlatformIO's **Quick Access** menu, expand **PIO Home**, and select **Devices**.
2) Choose the icon next to the port with the description **CP2104 USB to UART Bridge Controller** (this is usually `COM3`). Copy the device port number.

{{% notice note %}}
If your AWS IoT EduKit does not show up in the device list, confirm that it's powered on and you are using the supplied USB-A to USB-C cable. Some USB-C hubs have compatibility issues with establishing a serial port.
{{% /notice %}}

## Next
Now that your host machine can communicate with the AWS IoT EduKit reference hardware, let's continue to the next chapter — [**Run the ESP RainMaker Agent**](/en/getting-started/run-rainmaker.html).

---
{{% button href="https://github.com/aws-samples/aws-iot-edukit-tutorials/discussions" icon="far fa-question-circle" %}}Community support{{% /button %}} {{% button href="https://github.com/m5stack/Core2-for-AWS-IoT-EduKit/issues" icon="fas fa-bug" %}}Report bugs{{% /button %}}