.. _cob35_emergency:

=============================
 Releasing the emergency stop
=============================

After booting and during normal operation it can happen that the emergency stop gets issued
due to a number of things (even non critical), e.g.:

- Someone stepping too close to the robot (even if the robot does not move)
- The robot drives too close to an obstacle
- The wireless emergency stop gets disconnected
- Someone presses the emergency stop

In order to re-activate the robot, the wireless emergency device has to be
reconnected and the robot's modules have to be reset. Please follow these steps:

.. warning:: **Remove all obstacles and check surroundings first**

.. warning:: If the robot has been moving using the navigation, its goal might still be set **and the robot immediately tries to reach it**. If in doubt, restart the navigation module.


#. Press the wireless emergency button (if not done already)
#. Release the robot's emergency buttons (if pressed before)
#. Release the wireless emergency button

   A. Release red cap
   #. Press and hold green button on wireless emergency device

      *green light starts to blink*

   #. Turn power key on robot clockwise and release it after a few seconds

      *you hear "emergency button released" (only if ros bringup already running)*

   #. Release green button on wireless emergency device

#. Recover robot modules you intend to use in the dashboard's command gui
