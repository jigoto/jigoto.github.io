---
title: Cisco WAP Firmware Upgrade 3800 series 
description: This is a step-by-step manual on how to upgrade your Cisco AP firmware
author: Genki Gankio
date: 2024-08-23 01:00:00 +0800
categories: [Networking, Troubleshooting]
tags: [cisco, networking]
pin: true
math: true
mermaid: true
image:
  path: /assets/img/cisco.jpg
  alt: Photo by Kvistholt Photography from Unsplash
---


# CAPWAP to Mobility Express
{: .mt-4 .mb-0 }

## Factory resetting access point
{: data-toc-skip='' .mt-4 .mb-0 }

1. Connect console to a laptop (non-domain joined preferred).

2. Connect PoE to a guest or lab network.

3. Open up a Putty and connect through serial.

4. When connected, wait until device has completely booted.

5. From the access point, press the MODE button (as the photo below) for at least 20 seconds. You should be able to see the seconds count from the CLI.

![Desktop View](/assets/img/cisco-ap1.png){: width="972" height="589" }
Image-1


6. Wait until it says it is finished.


## Upgrade firmware from CAPWAP to Mobility Express
{: data-toc-skip='' .mt-4 .mb-0 }

1. Make sure you have the latest ME firmware saved in your PC. Check the file server or ask someone for confirmation.

2. Open up a TFTP server, locate the directory of the location where the .tar file is.

3. From the CLI, login to the device. After the device has been factory reset, you should be able to login as the default username and password ( Username:Cisco, Password: Cisco ; note that this is case-sensitive)

4. Enable the CLI, and type the following command.

```text
ap-type mobility-express tftp://serverip/filename
```

5. After entering the command, this should also show in the TFTP server that the transfer is ongoing.

6. Wait until it is finished. This will take a few minutes to finish.

7. Check version to confirm.

*Note: When the AP keeps booting up on a loop, stop access point from keep restarting. You can enter the command below.


```text
logging console disable
```


## Update your Cisco wireless access point firmware
{: data-toc-skip='' .mt-4 .mb-0 }


1. Download portable [**TFTPD64**](https://bitbucket.org/phjounin/tftpd64/downloads/)

2. Copy down the correct CISCO firmware ZIP file

3. Extract the ZIP file on the local machine

![Desktop View](/assets/img/cisco-ap2.png){: width="972" height="589" }
Image-2

4.  Run the portable TFTPD64 application and set the TFTPD local folder location to the root of the unzipped folder

![Desktop View](/assets/img/cisco-ap3.png){: width="972" height="589" }
Image-3

5. Use TFTP in the GUI to update:


![Desktop View](/assets/img/cisco-ap4.png){: width="972" height="589" }
Image-4

6. *Select Auto Restart to have AP automatically reboot — USE for single AP installations ONLY.

You should see the AP pulling down the matching hardware version firmware file via TFTP:


![Desktop View](/assets/img/cisco-ap5.png){: width="972" height="589" }
Image-5


> Use this command below if you are upgrading from `CAPWAP` to `Mobility Express`
{: .prompt-tip }


```text
ap-type mobility-express tftp://IP_ADDRESS/SW_NAME
```

> Use this command below if you are upgrading from `Mobility Express` to `Mobility Express`
{: .prompt-tip }


```text
archive download-sw /reload tftp://IP_ADDRESS/SW_NAME
```


Please support me through [**BuyMeACoffee**](https://www.buymeacoffee.com/genkiganko) and for more tech blog contents and upcoming merchandise!
