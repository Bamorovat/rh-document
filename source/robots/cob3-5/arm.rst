.. _Issue: https://gitlab.com/uh-adapsys/rh-hardware/issues/1
.. _PowerCube software: https://schunk.com/us_en/services/tools-downloads/software/
.. _CAN-USB/2: https://esd.eu/en/products/can-usb2
.. _CAN-USB Mini: https://esd.eu/en/products/can-usb-mini
.. _CAN-USB/2 drivers: https://esd.eu/en/software-downloads/27071

.. |internal-wiring| image:: /images/cob3-5/arm-internal-wiring.png
   :scale: 15%
   :alt: Photo of Care-o-bot arm CAN board wiring
   :align: middle

.. |external-wiring1| image:: /images/cob3-5/arm-external-wiring1.jpg
   :scale: 7%
   :alt: Photo of Care-o-bot arm external wiring
   :align: middle

.. |external-wiring2| image:: /images/cob3-5/arm-external-wiring2.jpg
   :scale: 7%
   :alt: Photo of Care-o-bot arm external wiring
   :align: middle

.. |external-wiring3| image:: /images/cob3-5/arm-external-wiring3.jpg
   :scale: 7%
   :alt: Photo of Care-o-bot arm external wiring
   :align: middle

.. |external-wiring4| image:: /images/cob3-5/arm-external-wiring4.jpg
   :scale: 7%
   :alt: Photo of Care-o-bot arm external wiring
   :align: middle

.. |powercube| image:: /images/cob3-5/arm-powercube.png
   :scale: 15%
   :alt: Photo of Care-o-bot arm CAN board wiring
   :align: middle

.. |board-front| image:: /images/cob3-5/arm-board-front.png
   :scale: 25%
   :alt: Care-o-bot arm CAN board (front) with wiring
   :align: middle

.. |board-back| image:: /images/cob3-5/arm-board-back.png
   :scale: 15%
   :alt: Care-o-bot arm CAN board (back) with fuses
   :align: middle

.. |motor-fuse| image:: /images/cob3-5/arm-motor-fuse.jpg
   :scale: 15%
   :alt: Screenshot with Care-o-bot arm fuse specification
   :align: middle

.. |canusb| image:: /images/cob3-5/canusb.jpg
   :scale: 10%
   :alt: Care-o-bot tray joints
   :align: middle

.. _cob35_arm:

==================
 Repairing the arm
==================

If you are unable to use the arm mounted on :ref:`cob3`, you may want to check
with the appropriate tools from the manufacturers if the hardware is responding properly.
Afterwards, it might become necessary to disassemble the arm and check or replace parts of
the hardware.

---------------------------------
Using the manufacturer's software
---------------------------------

To read the arm's status using the manufacturer's software, you need the following items:

- Windows (10) Computer/Laptop with internet connection (for downloads)
- An esd `CAN-USB/2`_ device (confirmed working but `CAN-USB Mini`_ might also work):

  |canusb|

- Matching USB cable (probably type A <-> type B)

Download and install the following software:

- `CAN-USB/2 drivers`_ from esd (free account required)
- `PowerCube software`_ from Schunk

To investigate the error, follow these steps:

#. Connect the `CAN-USB/2`_ device to your computer
#. Disconnect the arm's serial cable from the robot at ``CAN 4``
#. Connect the cable to the `CAN-USB/2`_ device
#. Check joint states with :program:`PowerCube`:

|powercube|

You can tell whether the joint is on-line and has power by looking at the state field.
In the above example, joint number ``01`` does not have power (red) but the controller is working fine (green).
The other joints can be accessed by selecting the appropriate tab in the top of the application (blue).

---------------
Arm disassembly
---------------

To disassemble the arm, you need the following devices:

- Allen key set
- Electronic screwdriver set
- Camera or mobile phone

.. warning:: Before you modify anything, be sure to take pictures of how things looked when still assembled.

In case you mixed up something, you can find reference pictures of the arm wiring and a connection board here as well.

Remove the arm from the robot
-----------------------------

.. warning:: Do not disassemble the arm alone, work in a pair of two people!

Follow these steps:

#. Take photos of the wiring between the arm and the robot
#. Disconnect all wires between the arm and the robot
#. One person loosens the arm's screws with an allen key while the other person fixates the arm
#. Place the arm on a firm surface

Wiring of the arm at the robot:

|external-wiring1|
|external-wiring2|
|external-wiring3|
|external-wiring4|

Remove the connection board
---------------------------

Follow these steps:

#. Take photos of the wiring
#. Disconnect the wires on the front side using the screwdriver
#. Carefully pull the connection board towards you, some pins are still plugged into the board from behind

Wiring of the front side of the connection board:

|board-front|
|internal-wiring|

---------------------
Replace a broken fuse
---------------------

If you suspect a broken fuse like in the above example, you have to disassemble the arm first.
Additionally, you need the following devices:

- A multimeter
- Two soldering irons with small tips

In the arm of :ref:`cob3`, there are two fuses located at the flip side of each connection board.
You can check if they are working with the multimeter.

|board-back|

When replacing the fuse, make sure you replace the correct one.
One ``15A`` fuse is for the motor, while the ``1A`` fuse belongs to the controller.
Both should be soldered on two pads at the same time (use preferred a customized soldering tip or two small soldering tips).
See below snapshot from the supplier's store depicting the ``15A`` fuse model that is used in the robot.

|motor-fuse|
