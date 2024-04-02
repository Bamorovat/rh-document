.. _API: http://doc.aldebaran.com/2-5/dev/programming_index.html
.. _Autonomous life: http://doc.aldebaran.com/2-5/family/pepper_user_guide/life_pep.html
.. _Choregraphe: http://doc.aldebaran.com/2-5/software/choregraphe/index.html
.. _team: https://robothouse.herts.ac.uk/team/

.. _pepper_startup:

============
 Starting up
============

Please follow these instructions when switching on :ref:`pepper`.
This page describes how to physically start the robot and what software needs to be launched.
Moreover, it provides checklists to ensure a successful startup.

Before Checklist
================

Ensure that
 - Robot is sufficiently charged.
 - The charging device is disconnected.

Hardware
========

#. Press the robot's power button at its chest (below the tablet).

    *Touchscreen displays SoftBank logo, head LEDs change colours.*

#. Wait for booting to complete.

    *Touchscreen displays colourful pattern. Bootup sound plays.*

    .. note:: Depending on the configuration (off by default), the robot also *wakes up* and calibrates.


Software
========

.. note:: The robot can be started with `Autonomous life`_ either enabled or disabled. For not conflicting with studies and demonstrations, we disable it by default.

The robot's essential components (i.e., basic bringup, perception) *are automatically started with the robot*. The robot instance (called :program:`NaoQI`) can be accessed using the `API`_, or `Choregraphe`_. *Autonomous life* can also be re-enabled using these methods as well the robot's web interface (by entering its IP address or host name into a browser).

Study/demo computer
-------------------

You can use any computer that is connected to the house's network and correctly configured to communicate with the robot's :program:`NaoQI` instance.
In most cases though, you would probably prefer to use one of the workstations inside Robot House (see :ref:`network`), typically :term:`char` in the living room, :term:`shakuras` in the office, or :term:`tarsonis` in the bedroom.
All of them should be configured correctly and have the necessary software installed, including :program:`Choregraphe` and the :program:`SDK` which provides the `API`_.

.. note:: Please contact the key `team`_ members if you need to request access to the robot from your personal account.

#. Setup your terminal's :ref:`robot_env` to :ref:`pepper` (and common robot house infrastructure) and set a :ref:`ros_ip`:

   .. code-block::

      $ robot_env common pepper
      $ ros_ip

   .. note:: Make sure to configure each terminal in which you plan to run software that communicates with the robot.

#. If you need to use :program:`Choregraphe`:

    #. Start the application:

       .. code-block::

         $ choregraphe-bin

    #. Connect to the robot:

      #. Select :menuselection:`Connection -> Connect to...`.
      #. Check :guilabel:`Use fixed IP/hostname`.
      #. Enter the robot's host name or IP address (see above).
      #. Click :guilabel:`Select`.

    *The robot view on the right briefly initialises and soon after resembles the real robot.*

#. Start any additional components that you are using for behavior generation.
