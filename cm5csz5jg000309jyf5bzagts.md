---
title: "Flipper Zero Guide for Beginners"
seoTitle: "flipperzero"
datePublished: Tue Dec 31 2024 18:29:45 GMT+0000 (Coordinated Universal Time)
cuid: cm5csz5jg000309jyf5bzagts
slug: flipper-zero-guide-for-beginners
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1735669740644/b243d0a3-a824-41fa-94c1-071c9a14719d.jpeg
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1735669767376/77b9ab3b-3c7d-41c9-8007-1c2a3f8be992.jpeg

---

Flipper Zero has become very popular among cybersecurity professionals, but what exactly is it? According to the device’s creators, Flipper Zero is your “cyberphile,” but that doesn’t explain much about how you’ll use it.

With this tutorial on Flipper Zero, you will learn that it is a tool that will greatly help you in the art of penetration testing in a natural environment. It’s also a fun tool to get started in the world of software-defined radio.

# **Flipper Zero Beginners Guide**

Let’s start the guide. First we will prepare your Flipper Zero and get it ready for use. Next, we’ll look at the basic features and interface. Next, we’ll tackle three step-by-step projects: cloning RFID access cards, creating BadUSB and DuckyScripts, and finally, cloning a garage opener. Starting with the guide for Flipper Zero

Now that you have Flipper Zero in your hands, let’s get started with the first instructions.

Before you start, you need to make sure you have a high-quality microSD card. It must be at least 4GB in size and formatted in the FAT file system. Insert it with the chip facing up.

It’s probably best to charge your Flipper first by plugging it into a USB power bank or your computer’s USB port to power it up. You can activate it by holding the back button for three seconds.

# **Hardware update**

After activating Flipper Zero for the first time, you will probably need to update your device’s hardware. When we opened ours, he asked us to.

There are two ways to update the hardware: using the mobile app or through the desktop app (qFlipper).

![](https://miro.medium.com/v2/resize:fit:1050/0*OVKa7epxIoLh6PeG align="left")

It is important to note that there are three hardware versions that you can choose from:

* The fixed version
    
* The release candidate
    
* The development version
    

The stable version has been extensively tested and is therefore recommended for most users. If you want something a little more up-to-date than the stable version, you can try the release candidate version. However, it may contain bugs before the final stable version is made.

Finally, the development version represents the cutting edge of technology, often being released several times a day, so don’t expect this hardware version to be stable on every download.

Regardless of whether you are using the mobile app or the desktop app to perform the update process, the task is similar in both cases. For this example, we’ll demonstrate using the qFlipper desktop app, so make sure you’ve connected Flipper Zero to your computer or mobile device via a USB-C cable.

Updating is a simple three-step process:

1. After downloading the program, launch it and click on the wrench-like button titled “Advanced Controls.”
    
2. Next, select “Hardware Update Channel” from the drop-down menu, choose the appropriate version you want to install on your Flipper Zero, and finally, click the button that says “Update.”
    

![](https://miro.medium.com/v2/resize:fit:1050/0*_4tPutjlLQ7VJ9QW align="left")

Once you click the update button, the device will go through a series of reboots before finally showing you an update success screen on the device and the qFlipper app or mobile app.

![](https://miro.medium.com/v2/resize:fit:1050/0*Rnr_fhypUX2pmwze align="left")

# **Custom Firmware**

Flipper Zero has many additional extensions and can also be customized to work in ways that the original makers, Flipper Devices, did not foresee.

Because of these capabilities, Flipper has made the device open to allow third parties to write custom hardware. This means you can download hardware from other providers to extend Flipper’s capabilities in many ways.

For example, Xtreme firmware is a popular extension version that allows customization of the interface, protocols and other features.

However, a word of warning about third-party hardware: any version other than the stable version should be considered non-stable and, although unlikely, could cause irreparable damage to your Flipper or have unforeseen consequences.

# **How to Use Flipper Zero: Basic Functions and Features**

Let’s take a moment to discuss how we can navigate the Flipper Zero interface.

**Flipper Buttons and Menus**

Although Flipper is a powerful device with many different applications, navigating the various menus is relatively simple. There are two main buttons and a directional pad.

* **Button 1:** It is located in the center of the directional pad and is mainly used for positive actions, such as performing a function or entering a new menu.
    
* **Button 2:** It has a back arrow that is used to cancel an action or return from a menu, with the directional pad providing appropriate navigation assistance.
    

For example, to use Flipper’s RFID function, simply press the main button (the one in the center of the directional pad) and use the up/down buttons until you reach the “125 kHz RFID” option.

Press the main button again and you’ll see a sub-menu (ours has four options), which is specifically related to using the RFID function (Read, Stored, Add Manually, and Additional Actions).

Finally, if Flipper Zero crashes for any reason, you can restart it by holding down the left and back buttons for five seconds.

**Basic functions**

Flipper Zero can be used to better understand how many software- and proximity-based technologies work, and use it for various tasks of simulating or replicating these technologies.

Technologies supported by Flipper include:

* **Radio Frequency Identification (RFID):** Often used in proximity cards for access control systems.
    
* **Control of wireless devices in the sub-1 GHz band:** It is used in many end devices such as garage doors, IoT sensors and doorbells, as well as smart devices such as light bulbs. While car remotes often operate in this frequency band, most modern cars use rolling-code encryption technology, making it impossible to use the Flipper Zero to lock or unlock cars.
    
* **Near Field Communication (NFC):** It works similarly to RFID technology, providing access to higher-frequency proximity cards — for example, a prepaid bus pass or a contactless credit card uses NFC.
    
* **Bluetooth:** A known low-range RF technology supported to enable Flipper Zero to connect to third-party devices and smartphones.
    
* **Infrared:** Flipper Zero has a built-in signal library for controlling common devices such as TV, air conditioner and stereo remote controls. Alternatively, you can program Flipper to understand other IR sequences using another remote control.
    
* **iButton:** Also known as 1-Wire keys, these are often used in door access control systems. This is quite an old technology, but it is still used worldwide. As the 1-Wire protocol has no authentication process, the Flipper Zero can easily read and store the keys in its memory.
    
* **USB Type-C:** Although the main purpose of the USB port is to charge or upgrade the device, it can also be used to provide USB signals to other devices using the BadUSB method.
    
* **Expandability:** Flipper Zero can be expanded in many ways — similar to a Raspberry Pi or Arduino — using general-purpose inputs/outputs (GPIOs). Flipper Zero already has some expansions, such as the official Flipper Zero WiFi development board, sub-1 GHz band expansion boards, and SAM expansion boards with HID Seos and iCLASS. These can greatly enhance the use of Flipper Zero for red teaming purposes.
    

# **Hacking Attacks with Flipper Zero**

What can you do with Flipper Zero? Now that we are ready, let’s get into some hacking projects with Flipper Zero.

**RFID Access Card Cloning**

In this example, we will copy or “clone” an RFID access card. RFID access cards are widely used worldwide, mainly to replace physical keys. Note that some RFID cards come in the form of a circular key fob, but generally work the same way as cards.

# **What Is RFID Technology?**

Radio Frequency Identification (RFID) is a technology that uses magnetic fields to automatically identify and track tags attached to physical objects.

These tags contain electronically stored information and can be passive — powered by the electromagnetic field generated by the reader — or active, with their own power source. RFID is used in a variety of applications, such as access control, inventory management, and even passports and contactless payment systems.

**Basic information**

After cloning an RFID card, we can reproduce the RFID information from our Flipper Zero, eliminating the need to use the RFID card, or clone it to another RFID card of the same type, instead of the original one. This means that we no longer need to have the original card to open the desired door.

# **How to Clone an RFID Access Card**

1. First, enter the main menu by pressing the main button, which is located in the center of the D-pad. Scroll down until you see the “125 kHz RFID” option and press the main button again. You will see the “Read” option at the top of the submenu.
    
2. With the access card you want to clone ready, place it under your Flipper Zero. Press the main button to read the card. Within a few seconds, you should hear a sound and display information about the type of card read.
    
3. Then press the right directional pad on the D-pad, and you’ll be presented with three options: “Save,” “Simulate,” and “Record.” If you want to save the RFID key values ​​for future use, press the main button under “Save.”
    

![](https://miro.medium.com/v2/resize:fit:1050/0*KzA6ZeJuVOKyy1o8 align="left")

If you want to use the new stored RFID values ​​immediately, select “Simulate.” If you want to clone the RFID card you just read to another RFID card or key fob, simply use the D-pad to select “Enroll” and press the main button.

Place the Flipper Zero over the new card or key fob and within a few seconds you will see “Registration Successful” appear on the screen. You have now cloned a key.

If you have saved the key values ​​in Flipper Zero, instead of writing them to an RFID key fob, you can return to the “Saved” menu at any time, select the card you saved, press the main button and select “Simulate” to play the RFID data to the desired receiver.

# **BadUSB and DuckyScripts**

In this example, we will use the BadUSB demo script provided in Flipper Zero to demonstrate the capabilities of a BadUSB attack. You can create your own BadUSB “DuckyScripts” or find ready-made scripts online to perform a variety of attacks.

**What Is BadUSB/KBUSB?**

Most of Flipper Zero’s functions are based on radio frequency technology. However, BadUSB is a security exploit that uses USB to execute malicious code on a computer without the user’s knowledge.

It takes advantage of the trust computers have in USB devices — especially the keyboard, which needs no setup before use. This makes BadUSB a powerful tool for cyber-attacks, such as spreading malware or destroying user inputs.

BadUSB was first revealed in 2014, but was popularized by Hak5 when they released the USB Rubber Ducky, a simple USB stick that pretended to be a keyboard using USB enumeration techniques.

Rubber Ducky provided a simple programming language called “DuckyScript,” which allowed users to perform automated payloads such as credential extraction, remote code execution, terminal access, and more.

**Basic information**

The DuckyScript language is a simple yet flexible language that allows you to deploy payloads to a target computer via a “Rubber Ducky” USB stick or, in this case, Flipper Zero.

The payloads available at [official GitHub of Rubber Ducky](https://github.com/hak5/usbrubberducky-payloads) they include code for remote access, command execution, data extraction, and even cell phone-based exploits, among many others.

![](https://miro.medium.com/v2/resize:fit:917/0*HffSSLJuXP8mfH89 align="left")

# **How to Execute an Attack**

If you want to create your own DuckyScript for the BadUSB attack or download one created by others, you will need to copy it to the microSD card.

Carefully remove your card from the Flipper Zero and insert it into your computer. In our case, we had to use a microSD adapter.

In your computer’s file explorer, you should see your SD card listed — ours is simply named NONAME. Inside the card folders, you’ll find a folder called **badusb**.

Just copy your DuckyScript payload into this folder. You might want to rename it to something that will help you remember it.

![](https://miro.medium.com/v2/resize:fit:1050/0*SPmSLGCGTCtbUEGi align="left")

Once you’ve copied your payloads to the MicroSD card, make sure to safely remove it from your computer’s operating system, then carefully insert it back into the Flipper Zero. Cards can break easily!

![](https://miro.medium.com/v2/resize:fit:1050/0*gERKBDHspZSfznNu align="left")

Once the card is inserted, connect the USB cable to the Flipper Zero and the other end to your target computer. Press the main button and use the up/down buttons in the main menu until you find the option “Bad USB.”

Press the main button and you will see the various payload files located in the “badusb” folder of your microSD card, including the one you just copied. Scroll up/down to select the payload you want to run.

![](https://miro.medium.com/v2/resize:fit:1050/0*wf-0a6SbDr504xc_ align="left")

In this example, we use the payload **demo\_macos** provided with Flipper Zero. Press the main button on your selected payload.

![](https://miro.medium.com/v2/resize:fit:1050/0*AkorMKCPV-m3ls28 align="left")

When you have connected the USB cable to both the Flipper Zero and the target computer, you will see an image similar to the one above. Now, just press the main button to run the payload.

![](https://miro.medium.com/v2/resize:fit:1050/0*zZ4-iiqTxLwmVqXO align="left")

If the payload script is working correctly, you should see a progress bar like the one shown above.

![](https://miro.medium.com/v2/resize:fit:1050/0*cTVUle4bHTVZHm3f align="left")

# **Garage Door Card Cloning with Sub-GHz Wireless**

In this exercise, we will clone a garage door opener from up to 35 meters away. Flipper Devices claims it can work up to 50 meters, but results may vary.

**What Is Sub-GHz?**

Sub-GHz refers to wireless communication frequencies that are below 1 GHz.

These frequencies are commonly used for long distance communication because of their ability to penetrate obstacles and cover longer distances with less power compared to higher frequencies.

Sub-GHz communication is widely used in applications such as remote control systems, IoT sensors, doorbells, smart lamps and meters.

**Basic information**

To perform this cloning, we will need to have access to the original garage door opener, or at least be present when the garage door opens.

Garage door openers usually have less encryption than modern car remote controls, so it’s more likely to succeed, especially on older ones.

What we should note is that newer garage door openers use something called “rolling code encryption.” If your garage door uses this technology, then it will not work with your Flipper Zero.

# **How to Perform the Procedure**

First, enter the main menu by pressing the main button in the middle of the D-pad and scroll up or down until you find the option “Sub-GHz.”

![](https://miro.medium.com/v2/resize:fit:782/0*yP1SElmYxkPl8b-m align="left")

Then move the D-pad down to the “Frequency Analyzer” option and press the main button. Press the garage door button and note the frequency the remote is transmitting. If you have a two-button remote, press the second button to note that frequency as well.

![](https://miro.medium.com/v2/resize:fit:1050/0*teWJpj-JnvGRgagf align="left")

Now, press the back button and select “Read RAW.” You will see a frequency log image.

![](https://miro.medium.com/v2/resize:fit:1050/0*ULqvmaV9tXBAjBB4 align="left")

![](https://miro.medium.com/v2/resize:fit:1050/0*vK8P-408P8RwGW7U align="left")

Press the left arrow on the D-pad to select “Setup” and set the frequency you noted earlier. If you have more than one button with a different frequency, you will need to repeat this process.

![](https://miro.medium.com/v2/resize:fit:1050/0*IqDsYnGnBGdmjVoB align="left")

You can change the frequency values ​​to match the ones you found in the frequency analyzer using the left and right keys.

Then press the return button and Flipper Zero will return you to the frequency logger you saw when you selected “Read RAW.” Press the main button and the recording will start.

Press the garage door button again and you will notice that the display shows the frequency reading via a “spike” in the image.

![](https://miro.medium.com/v2/resize:fit:1050/0*-zMyKvFpVL2TJeEO align="left")

Now that you have recorded the signal, you can either press the “Save” option by pressing the right button to save this signal and use it later, or if you want to send it directly to the receiver, you can use the “Send” option ” by pressing the main button.

![](https://miro.medium.com/v2/resize:fit:1050/0*nghtg73GeWZTeHZf align="left")

![](https://miro.medium.com/v2/resize:fit:1050/0*7xOPgEI6rlggrSHe align="left")

Please note that some frequencies may not be allowed to broadcast in your area using the original Flipper Zero firmware.

# **Conclusions**

Flipper Zero is a great tool that reveals the world of Software Defined Radio (SDR), a world that often remains incomprehensible to non-builders or members of the SDR hacking world.

With Flipper Zero, this field is now more accessible and exciting for hobbyists and hackers.

Many have mistaken the Flipper Zero as a device designed for malicious uses. However, it can be seen as an educational, multifunctional tool that combines SDR and the experimental process in a fun way.

As with most tools, if people want to use them illegally, they will often find a way.

If you are interested in understanding the world of Software Defined Radio in the form of a multi-tool, Flipper Zero is an excellent, user-friendly introduction to this world. Plus, it makes a great topic of conversation with friends at the dinner table.

thank you😊

Ferdi Birgül