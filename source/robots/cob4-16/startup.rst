.. _team: https://robothouse.herts.ac.uk/team/

.. _cob4_startup:

============
 Starting up
============

Please follow these instructions when switching on :ref:`cob4`.
This page describes how to physically start the robot and what software needs to be launched.
Moreover, it provides checklists to ensure a successful startup.

Before Checklist
================

Ensure that:
 - Robot and its :ref:`cob4_remote` are fully charged.
 - Wireless emergency stop is fully charged.
 - Brake release is not pressed (so that the red button inside the robot is on and not pulsating).
 - The charging device is disconnected.

Hardware
========

#. Open the robot's lid at its base.
#. Press the power button.

    *LED becomes green, robot powers on and its computers begin to boot up.*

#. Close the lid again.
#. Wait for the robot and its components to boot up completely.

    *LED ring at the robot base pulsates in a cyan colour.*

    .. note:: Booting can take up to **five minutes**, please be patient.

#. Complete all of :ref:`cob4_recovery` to initialize the robot's modules.

Software
========

Some components (i.e., basic bringup, navigation, perception, :ref:`cob4_remote`) have to be started on the robot, others (e.g., visualization, behaviour control) on your desired study/demo computer.

You can use any computer that is connected to the house's network and correctly configured to use the robot's roscore to start behavioral components.
In most cases though, you would probably prefer to use one of the workstations inside the robot house (see :ref:`network`), typically :term:`char` in the living room, :term:`korhal` in the office, or :term:`tarsonis` in the bedroom. All of these computers are setup correctly and have the necessary software installed.

You can also log into the robot via :ref:`ssh` without having to type in a password from all Robot House computers if you are logged in as the :term:`demo` user.

.. note:: Please contact the key `team`_ members if you need to request access to the robot from your personal account.

On the robot
------------

The following components have to run on the robot's internal computer :term:`b1` to enable its basic functionalities and navigation. 

#. Log into the robot:

   .. code-block::
  
      $ ssh demo@b1
     
#. Use a ``screen`` session to allow the components to run detached in the background:

   .. code-block::
      
      $ screen

#. Start the ``bringup`` component to initialize the robot:

   .. code-block::

      $ roslaunch uh_cob bringup.launch
      
#. Press :kbd:`Ctrl + A,D` to detach the screen session and let the component run in the background.


Study/demo computer
-------------------

The following steps have to be followed on the Robot House computers:

#. Setup your terminal's :ref:`robot_env` to :ref:`cob4` and set a :ref:`ros_ip`:

   .. code-block::

      $ robot_env cob
      $ ros_ip

   .. note:: Make sure to configure each terminal in which you plan to run software that communicates with the robot.

#. Start :program:`RViz` for a robot visualization:

   .. code-block::

      $ roslaunch uh_cob rviz.launch

#. Start the dashboard for command execution (e.g., initialization, postures):

   .. code-block::

      $ roslaunch uh_cob dashboard.launch

#. Start any additional components that you are using for behavior generation.

After Checklist
===============

Ensure that :program:`RViz` is in sync with the robot:
 - Check the robot's position on the map (if you use the navigation). You can adjust the robot position and orientation by using the :guilabel:`2D Pose Estimate` button.
 - See whether the robot's posture is correct (esp. if you are using the arms). Verify that :ref:`cob4_recovery` have been successful for all components.

Check the robot's appearance:
 - Make sure that the robot is in its base posture as depicted in :numref:`fig_cob4`.
 - Confirm that the LEDs at the wheel covers are glowing in a cyan colour indicating that all components are working
