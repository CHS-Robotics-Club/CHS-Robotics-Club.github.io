---
layout: doc
title: Deploying to the Robot
slug: deploying
description: >-
  How to set up the robot for code deployment
---

* TOC
{:toc}

# Setting up the Robot

## Prerequesites

Windows is requires for this setup (preferably Windows 10). 

[Python3.x][Python Installation]{:target="_blank"} is also required (preferably \>3.8).

## Imaging

### Updating firmware and Formatting

There are two system-related operations that must be taken out before using the robot.

The first is ensuring that the firmware is up to date. Firmware is the low level interface between the actual robot's hardware and the software, allowing certain low level functions to be completed with ease, usually with the help of even more interfaces.

The second is ensuring that the robot is correctly formatted. This is like putting an operating system on the robot, so that programs like python may be run and so that you can communicate to it via its networking interface. What is actually put onto the robot is called an **image**, and is in the format of a `.zip` file.

### Installing necessary tools

All the necessary files are packaged in the **[FRC Game Tools installer]{:target="_blank"}**, which must be reinstalled every year. Following this installer should install both the latest firmware and image. However, these are not installed on the robot just yet, only on the computer. To upload them to the robot, we need to use the **FRC roboRIO Imaging Tool**, which is also installed with the FRC Game Tools.

### Connecting to the Robot

The method of communicating to the robot is using the robot's network, which is emitted from the robot's **Radio**. This should already be set up, but if it is not, see the documentation for *[Programming your Radio]{:target="_blank"}*. 

![Radio]{: height="150rem"}

_Radio_

To turn on the radio, the robot must be turned on. To turn it on, press the switch on the **circuit breaker**. It should be a sort of lever that pushes horizontally, not the red button.

![Circuit Breaker]{: height="150rem"}

_Circuit Breaker_

Once the radio is on, you can connect to it from your computer's network (the place where you connect to wifi). One windows, this will be available in the bottom right near the sound icon. The title of the network should be the team code: **2827**. Note that you will not be able to use the internet while connected. 

Once connected, open the **roboRIO Imaging Tool** (it should be available by searching, but, if you cannot find it, it should be at this location on the machine: `C:\Program Files (x86)\National Instruments\LabVIEW YYYY\project\roboRIO Tool`). If you are properly connected to the robot's network, the robot should appear the *roboRIO Targets* list. 

![roboRIO Imaging Tool]{: width="50%"}

_roboRIO Imaging Tool_

### Updating the firmware

Make sure you have selected your robot from the *roboRIO Targets* list in the *roboRIO Imaging Tool*.

The firmware does not need to be updated every year. To see if the firmware needs to be updated, check the *Firmware Version* in the *System Information* panel in the bottom left make sure it meets the requirements stated in [the documentation][Updaing Firmware Documentation]{:target="_blank"}. If it says "Update Required" next to *Firmware Version*, it does need to be updated. 

To update the firmware, press the *Update Firmware* radio box in the top right, enter the *Team Number* 2827, select the latest firmware target in the *Select Firmware* box (the one with the largest number), and press the *Update* button in the bottom right.

### Imaging the robot

Make sure you have selected your robot from the *roboRIO Targets* list in the *roboRIO Imaging Tool*.

The robot needs to be reformatted every year, and sometimes multiple times if the version changes. To check the current image's year and version, find the *Current Image* in the *System Information* panel in the bottom left. It should have the format: `FRC_roboRIO_{YEAR}_v{VERSION}`.


To image the robot, press the *Format Target* radio box in the top right, enter the *Team Number* 2827, select the image corresponding to the season's year in the *Select Image* panel with the highest version (if this image is the same as the *Current Image*, you do not need to reformat), and press the *Reformat* button in the bottom right.

## Installing RobotPY

### (Optional) Setting up the Virtual Environment

Python has a feature called virtual environments that ensures that Python and all the installed modules are contained so that the code may be shared easily and consistently. They are not necessary to run the code.

Virtual environments are usually set up in the same folder as where the code is, so make sure to download the code if it is not already downloaded \[INSERT LINK HERE FOR DOCS ON DOWNLOADING CODE\].

To set up a virtual environment, first, open a command prompt window \[INSERT LINK HERE FOR DOCS ON USING COMMAND PROMPT\]. Use the command `CD` to go to the directory with the code  
(ex. `cd C:\Programming\Robotics\2021`). 

Virtual environments are usually set up in the `.venv` directory inside the folder with the code, where it stores the separate copy of the Python executable and the installed modules, as well as scripts to use the virtual environment. If there is no `.venv` directory, then run the python module to create a virtual environment: `python -m venv .venv`.

To use the virtual environment, you must run the script `activate.bat` inside the `Scripts` subdirectory of `.venv`. On Windows, this command should run that scrpit, assuming that the current working directory includes the `.venv` folder.

    .\.venv\Scripts\activate.bat

Now, when you run `pip` or `python`, the virtual environment versions will be used. 

To deactivate the virtual environment, you can either close the command prompt or run the `deactivate.bat` script.

    .\.venv\Scripts\deactivate.bat

You will need to run the activate script every time you open a new command prompt window and before every session of running code on the robot. 

### Installing necessary modules on the computer

Only one Python module is necessary to work with the robot: [RobotPy]{:target="_blank"}, the documentation for which can be found [here][RobotPy Docs]{:target="_blank"}. To install this module, run the command

    python -m pip install robotpy

This module installs Python bindings to the native WPILib library, which is used to communicate with the robot. Note that this command does not install all functionality, such as optional or vender specific components.

### Installing necessary modules on the robot

RobotPy gives you the ability to install items onto the robot using the `robotpy_installer` module. 

Two things will need to be installed on the robot: Python and RobotPy.

First, you will need to download both of them onto the local machine using these two commands

    python -m robotpy_installer download-python
    python -m robotpy_installer download robotpy

Then, with the robot turned on, you need to connect to the robot's network, which should be titled the team number: 2827.

Once connected, you can transfer these downloaded files onto the robot and install them with these two commands:

    python -m robotpy_installer install-python
    python -m robotpy_installer install robotpy

Note that these commands:

	python -m robotpy_installer download [module]
	python -m robotpy_installer install [module]
	
May be used for any Python modules (eg. Numpy).

The robot can now be deployed to.

# Deploying Code

Deploying code is relatively simple. 

Ensure that the robot is turned on and connect to its network. Once the network has connected, run the main file in the code directory (usually titled `robot.py` in the root directory) with the command line argument `deploy`:

    python robot.py deploy

You may have to press `y` when it asks if you want to upload large files. 

There are some optional command line arguments as well:

* `-nc` Gives you feedback with the Netconsole (recommended to not use due to threading issues)

Now the code is on the robot! 

# Running Code

The code on the robot is not activated without the **FRC Driver Station**, which is installed with the FRC Game Tools installer.

While connected to the robot's network, open the FRC Driver Station executable. To activate the code, you must press enable. Errors will show up on the right console, and you are able to switch between multiple modes on the left (teleoperated vs. autonomous).

[Python Installation]:https://www.python.org/downloads/
[FRC Game Tools installer]:https://www.ni.com/en-us/support/downloads/drivers/download.frc-game-tools.html
[Programming your Radio]:https://docs.wpilib.org/en/stable/docs/zero-to-robot/step-3/radio-programming.html
[Radio]:https://docs.wpilib.org/en/stable/_images/openmesh-radio-status-lights.png
[Circuit Breaker]:https://images-na.ssl-images-amazon.com/images/I/71UbR8ztPXL._AC_SL1500_.jpg
[roboRIO Imaging Tool]:https://docs.wpilib.org/en/stable/_images/roborio-imaging-tool.png
[Updaing Firmware Documentation]:https://docs.wpilib.org/en/stable/docs/zero-to-robot/step-3/imaging-your-roborio.html#updating-firmware
[RobotPy]:https://pypi.org/project/robotpy/
[RobotPy Docs]:https://robotpy.readthedocs.io/en/stable/