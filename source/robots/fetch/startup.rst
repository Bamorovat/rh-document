.. _team: https://robothouse.herts.ac.uk/team/

.. _fetch_startup:

============
 Starting up
============

Please follow these instructions when switching on :ref:`fetch`.
This page describes how to physically start the robot and what software needs to be launched.
Moreover, it provides checklists to ensure a successful startup.

Before Checklist
================

.. warning:: Before doing *anything* with :ref:`fetch`, always verify that the breaker switch at the back of the robot is set to  **on (I)**.

Ensure that
 - Robot and its :ref:`fetch_remote` are fully charged.
 - The charging device is disconnected.

Hardware
========

#. Release emergency stop button at the side (if not already released).
#. Press the power button.

    *LED around the switch becomes white, robot powers on and its computers boot up.*

#. Wait for the robot and its components to boot up completely.

    *Robot's arm should be in gravity compensation mode, i.e., easy to move.*

#. Connect the remote control to the robot by pressing the round central button.

    *Remote vibrates as it connects, red LED indicates first channel is used.*

Software
========

Most components (i.e., basic bringup, navigation, perception, :ref:`fetch_remote`) *are automatically started* on the robot at boot time. Therefore, you normally do not need to access the robot's computer. You can run other components (e.g., visualization, behaviour control) on your desired study/demo computer.

Study/demo computer
-------------------

You can use any computer that is connected to the house's network and correctly configured to use the robot's roscore to start behavioral components.
In most cases though, you would probably prefer to use one of the workstations inside Robot House (see :ref:`network`), typically :term:`char` in the living room, :term:`shakuras` in the office, or :term:`tarsonis` in the bedroom.
All of them are configured correctly and have the necessary software installed.

You can also log into the robot via :ref:`ssh` without having to type in a password from all Robot House computers if you are logged in as the :term:`demo` user.

.. note:: Please contact the key `team`_ members if you need to request access to the robot from your personal account.

#. Setup your terminal's :ref:`robot_env` to :ref:`fetch` and set a :ref:`ros_ip`:

   .. code-block::

      $ robot_env fetch
      $ ros_ip

   .. note:: Make sure to configure each terminal in which you plan to run software that communicates with the robot.

#. Start :program:`RViz` for a robot visualization:

   .. code-block::

      $ roslaunch uh_fetch rviz.launch

#. Start any additional components that you are using for behavior generation.

After Checklist
===============

Ensure that :program:`RViz` is in sync with the robot
 - The robot's position on the map is correct (if you use the navigation). You can adjust the robot position and orientation by using the :guilabel:`2D Pose Estimate` button.
