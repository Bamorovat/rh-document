.. _cob35_startup:

============
 Starting up
============

Please follow these instructions when switching on :ref:`cob3`.
This page describes how to physically start the robot and what software needs to be launched.
Moreover, it provides checklists to ensure a successful startup.

Before Checklist
================

Ensure the following
 - The robot is fully charged
 - The robot's wireless emergency stop is fully charged
 - The robot's tablet is fully charged

Hardware
========

1. Remove the charger from the robot (red plug)
#. Turn the key on the robots back side to the right, hold it for three seconds, and then release it

    *robot powers on and its computers boot up*

#. Wait for bootup to complete

    *ubuntu login-sound can be heard*

#. Release the two emergency buttons at the robot (rotate and pull)
#. Release the wireless emergency button

   A. Release red cap on wireless emergency device
   #. Press and hold green button on wireless emergency device

       *green light starts to blink*

   #. Turn power key on robot clockwise and release it after a few seconds

       *you hear clicking noises*

   #. Release green button on wireless emergency device

   #. Repeat the last three steps

       *you hear "emergency button released" (only if the ROS components on the robot's first computer are already running, see below)*

Software
========

Some components (i.e., basics, navigation, perception) have to be started on different PCs of the robot, others (e.g., visualization, behaviour control) on your desired study/demo computer.

First robot computer
--------------------

The following components all have to run on :term:`cob3-5-pc1` to enable
the robot's basic functionalities and navigation (optionally):

.. note:: You need to log into the robot for each of the following commands individually using the following in a new terminal window:

   .. code-block::

      $ ssh cob3-5-pc1

#. Start ROS communication

   .. code-block::

      $ roscore

#. Start the bringup component to initialize the robot

   .. code-block::

      $ roslaunch cob_bringup robot.launch

#. Start the script server to execute commands/scripts on the robot

   .. code-block::

      $ roslaunch cob_script_server script_server.launch

#. Start the navigation component (if you want the robot to drive)

   .. code-block::

      $ roslaunch cob_navigation_global 2dnav_ros_dwa.launch

Second robot computer
---------------------

The following components have to run on :term:`cob3-5-pc2` to enable
robot vision:

#. Log into the robot's second computer

   .. code-block::

      $ ssh cob3-5-pc2


#. Start the image republisher (if you want camera images from the robot)

   .. code-block::

      $ roslaunch accompany_siena_images_republisher accompany_images_republisher.launch

Study/demo computer
-------------------

You can use any computer that is connected to the house's network and correctly configured to use the robot's ``roscore`` at ``http://cob3-5-pc1:11311`` (i.e. running Ubuntu 12.04 precise and ROS hydro) to start behavioral components.
In most cases though, you would probably prefer to use the legacy workstation inside the robot house office, named :term:`rh-desktop-n` as the :term:`demo` user as this should be configured correctly, has :program:`RViz` and the dashboard installed, and allows you to access the robot via :ref:`ssh` without having to type in a password.

6. Start :program:`RViz` for a robot visualization

   .. code-block::

      $ roslaunch cob_bringup rviz.launch

#. Start the dashboard for command execution (e.g., initialization, postures)

   .. code-block::

      $ roslaunch cob_bringup dashboard.launch

#. Initialize robot modules you intend to use in the dashboard's :program:`Command GUI`

#. Start any additional components that you are using for behavior generation

After Checklist
===============

Ensure that :program:`RViz` is in sync with the robot
 - Tray, arm and body are displayed in the correct position (after their initialization)
 - The robot's position on the map is correct (if you use the navigation)
