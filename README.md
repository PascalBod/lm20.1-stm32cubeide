#### Table of contents

* [Overview](#overview)
* [Prerequisites](#prerequisites)
* [VirtualBox installation](#virtualboxInstallation)
* [Creation of the VM](#creationOfTheVm)
* [VM configuration](#vmConfiguration)
  * [Reference documents](#referenceDocuments)
  * [STM32CubeIDE installation](stm32cubeideInstallation)
* [Sample application](#sampleApplication)
  * [Install sample applications](#installSampleAppications)
  * [Import a sample application](#importASampleApplication)
  * [Flash and run the application](#flashAndRunTheApplication)

<a name="overview"></a>
# Overview

This short tutorial describes a way to make a virtual machine configured for STM32 software development with STM32CubeIDE, and explains how to use it. The virtualization environment is VirtualBox, and the guest machine runs Linux Mint 20.1.

<a name="prerequisites"></a>
# Prerequisites

* Hardware: a 64-bit computer with enough memory so that the VM can be granted 16 GB, with a few tens of GB available on the disk, and one free USB A port
* Hardware (bis): a [Nucle-L476RG board](https://www.st.com/content/st_com/en/products/evaluation-tools/product-evaluation-tools/mcu-mpu-eval-tools/stm32-mcu-mpu-eval-tools/stm32-nucleo-boards/nucleo-l476rg.html) with an USB A / micro USB B cable - any similar NUCLEO board can be used
* Developer: 
  * basic knowledge of Linux (knowing the most common commands...)
  * basic knowledge of VirtualBox (knowing how to create a virtual machine...)

<a name="virtualboxInstallation"></a>
# VirtualBox installation

[Download the VirtualBox binary package for your platform and install it](https://www.virtualbox.org/wiki/Downloads). Version at time of writing is 6.1.18.

Install the Extension Pack: it provides support for USB 2.0 and 3.0 devices.

<a name="creationOfTheVm"></a>
# Creation of the VM

[Download Linux Mint 20.1, MATE edition](https://linuxmint.com/download.php).

[Verify the integrity of the downloaded file](https://linuxmint.com/verify.php).

Start VirtualBox, and create a new virtual machine, using the Linux Mint ISO file previously downloaded. Set memory size to 16 GB and file size to 30 GB.

Wait for Linux desktop to be displayed.

If your keyboard layout is not QWERTY, click on the main-menu icon (the small icon displaying Linux Mint logo, in the lower left-hand corner), select **Control Center**, click on **Keyboard** icon, select **Layouts** tab, add the layout for your keyboard, and remove the existing **English (US)** layout. Close the Control Center windows.

Double click on the **Install Linux Mint** icon. Following information or selections can be provided, when required for:
* Language: English
* Keyboard layout: the one for your keyboard
* Install multimedia codecs
* Erase disk and install Linux Mint
* Name: Developer
* Computer's name: STM32LM
* Username: developer
* Password: choose one

At the end of the installation, restart. When you get the message **Please remove the installation medium, then press ENTER:**, click on Enter key.

Log in as *developer* user. Close the **Welcome to Linux Mint** window.

In the VirtualBox menu, select **Devices > Insert Guest Additions CD image...**. Double-click on the CD icon that appeared on the desktop. In the file explorer window, right-click on the **VBoxLinuxAdditions.run** file and select **Run as Administrator**. The password you are then asked for is the one you chose at installation time.

Once the guest additions are installed, you can right-click on the CD icon and select **Eject**.

Click on the system report icon, in the lower right-hand corner: ![icon](images/systemReportIcon.png). In the **System Reports** window that appears, select **System reports > Install language packs**, click on **Install the Language Packs** button, and accept the installation. The requested password is the one you chose at installation time.

For the system restore utility, click on **Ignore this report**. Close the window.

Click on the update manager icon, in the lower right-hand corner: ![icon](images/updateManagerIcon.png). In the welcome screen of the **Update Manager** window that appears, click on **OK** button. Click on the **No** button of the **Do you want to switch to a local mirror?** banner (you'll be able to choose one later on). If you are told that a new version of the update manager is available, click on **Apply the Update** button. Again, the requested password is the one you chose above (I won't say it anymore :-) ). Click on **Install Updates** button, and accept additional changes.

To grant access to the virtual serial link that will be used to program the NUCLEO board, add the user to the dialout group:

```shell
$ sudo adduser developer dialout
```

Reboot: main menu and **Quit > Restart**.

You can resize the VirtualBox window: the Linux Mint desktop will resize accordingly.

<a name="vmConfiguration"></a>
# VM configuration

<a name="referenceDocuments"></a>
## Reference documents

* [STM32CubeIDE documentation](https://www.st.com/content/st_com/en/products/development-tools/software-development-tools/stm32-software-development-tools/stm32-ides/stm32cubeide.html#documentation)
* [STM32CubeL4 documentation](https://www.st.com/content/st_com/en/products/embedded-software/mcu-mpu-embedded-software/stm32-embedded-software/stm32cube-mcu-mpu-packages/stm32cubel4.html#documentation)
* [STM32CubeIDE basics MOOC](https://www.st.com/content/st_com/en/support/learning/stm32-education/stm32-moocs/STM32CubeIDE_basics_MOOC.html)

<a name="stm32cubeideInstallation"></a>
## STM32CubeIDE installation

According to the [Installation Guide](https://my.st.com/resource/en/user_manual/dm00603964-stm32cubeide-installation-guide-stmicroelectronics.pdf):
* [Download STM32CubeIDE Debian Linux Installer 1.5.1](https://www.st.com/content/st_com/en/products/development-tools/software-development-tools/stm32-software-development-tools/stm32-ides/stm32cubeide.html). You will have to create an account
* Unzip the file
* Run resulting script:

```shell
$ sudo sh ./st-stm32cubeide_1.5.1_9029_20201210_1234_amd64.deb_bundle.sh
```

* Accept the license, install Segger J-Link udev rules, accept additional licenses

No need to perform the last step, the manual installation, described in the Installation Guide.

<a name="sampleApplication"></a>
# Sample application

<a name="installSampleAppications"></a>
## Install sample applications

* Start STM32CubeIDE, from Linux Mint main menu and then **All applications > Programming**
* Keep the default workspace and click on the **Launch** button
* Install the STM32 MCU Package for STM32L4 Series version 1.16.0:
  * Select **Help > Manage Embedded Software Packages**
  * On the **STMicroelectronics** tab, open the **STM32L4** list and select the package
  * Click on the **Install Now** button

The package is installed in `/home/developer/STM32Cube/Repository/STM32Cube_FW_L4_V1.16.0`.

<a name="importASampleApplication"></a>
## Import a sample application

* Click on the *Minimize* icon of the *Information Center* window, in the upper right-hand corner:

<img src="images/minimize.png">

* Select **File > Import...**
* Select **General > Import ac6 System Workbench for STM32Project**
* Click on the **Next >** button
* For **Import source**, select `/home/developer/STM32Cube/Repository/STM32Cube_FW_L4_V1.16.0/Projects/NUCLEO-L476RG/Examples/GPIO/GPIO_EXTI/SW4STM32/STM32L476RG_NUCLEO`
* Click on the **Finish** button
* Accept project conversion
* A project named *STM32L476RG_NUCLEO* appears in the *Project Explorer* window
* Click on the small vertical triangle at the left of the project name, in order to display project files
* Select **Project > Build Project**

At the end of the build, the **Console** window displays the result:

<a href="images/console.png"><img src="images/console-medium.png"></a>

The **Build Analyzer** window provides memory usage information:

<a href="images/buildAnalyzer.png"><img src="images/buildAnalyzer-medium.png"></a>

<a name="flashAndRunTheApplication"></a>
## Flash and run the application

Connect the NUCLEO board to the host PC. Check that the virtual machine can see it, with **Devices > USB** from VirtualBox menu. A new USB device should be visible: *STMicroelectronics STM32 STLink [0100]*. Tick the associated checkbox.

Assign the board to the virtual machine on a permanent basis:
* Select **Device > USB > USB Settings...**
* Click on the *Add new USB filter* button
* Select the board
* Click on the **OK** button

In the Project Explorer window, open the `Debug` directory and select `STM32L476RG_NUCLEO.bin`. This is the binary file to use to program the board.

Create a run configuration by selecting **Run > Run configurations...**. Select **STM32 Cortex-M C/C++ Application**. 
Click on the *New Launch Configuration* tool, above the list of configuration types. The various fields should be prefilled with the right default values:

<a href="images/runConfigurationsMain.png"><img src="images/runConfigurationsMain-medium.png"></a>
<a href="images/runConfigurationsDebugger.png"><img src="images/runConfigurationsDebugger-medium.png"></a>

Click on the **Run** button.

Depending on the version of the NUCLEO board, a window requesting an update of the ST-Link firmware may be displayed:

<a href="images/stLinkFirmwareVerification.png"><img src="images/stLinkFirmwareVerification-medium.png"></a>

Click on the **Yes** button.

The ST-Link upgrade window is displayed:

<a href="images/stLinkUpgrade.png"><img src="images/stLinkUpgrade-medium.png"></a>

Click on the **Open in update mode** button. The window displays firmware version information:

<a href="images/stLinkUpgradeUpdate.png"><img src="images/stLinkUpgradeUpdate-medium.png"></a>

Click on the **Upgrade** button. At the end of the upgrade, close the window.

Request again to run the above run configuration. The Console window displays a rebuild, the board programming, and ends with a message saying that the debugger connection is lost. That's normal, as we didn't start a debugging session.

Push on the blue button. The green LED should light up when you release the button. Push again, it should cut out when the button is released.