.. _cob4_recovery:

============================
 Initialisation and recovery
============================

After booting and during normal operation it can happen that the emergency stop gets issued
due to a number of things (even non critical), e.g.:

- The robot just booted up.
- Someone stepping too close to the robot (even if the robot does not move).
- The robot drives too close to an obstacle.
- The wireless emergency stop gets disconnected.
- Someone presses the emergency stop.

In order to re-activate the robot, the wireless emergency device has to be
reconnected and the robot's modules have to be reset. Please follow these steps:

.. warning:: **Remove all obstacles and check surroundings first!**

.. warning:: If the robot has been moving using the navigation, its goal might still be set **and the robot immediately tries to reach it as soon as the emergency stop is released**. If in doubt, restart the navigation module or cancel/restart all of ``roslaunch uh_cob bringup.launch``.


#. Release the two emergency buttons at the robot (if pressed).
#. Release the wireless emergency button (if pressed).

    *You hear "emergency button released" and an orange light appears behind the two buttons at the robot.*

#. Initialize the robot by pressing the ``upper right shoulder`` and ``start`` buttons at the same time on the remote controller.

    *You hear "init and recover", then <component name> for each component, and finally "go".*
