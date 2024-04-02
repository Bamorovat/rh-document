.. _Issue: https://gitlab.com/uh-adapsys/rh-hardware/issues/1
.. _MTS software: https://schunk.com/us_en/services/tools-downloads/software/
.. _CAN-USB/2: https://esd.eu/en/products/can-usb2
.. _CAN-USB Mini: https://esd.eu/en/products/can-usb-mini
.. _CANopen tools: https://esd.eu/en/products/canopen-protocol-stack-library
.. _CAN-USB/2 drivers: https://esd.eu/en/software-downloads/27071

.. |canusb| image:: /images/cob3-5/canusb.jpg
   :scale: 10%
   :alt: Care-o-bot tray joints
   :align: middle

.. |tray-wiring| image:: /images/cob3-5/tray-wiring.jpg
   :scale: 10%
   :alt: Care-o-bot tray joints
   :align: middle

.. |tray| image:: /images/cob3-5/tray.jpg
   :scale: 15%
   :alt: Care-o-bot tray joints
   :align: middle

.. _cob35_tray:

===================
 Repairing the tray
===================

If :ref:`cob3`'s tray position becomes misaligned with its virtual representation, it cannot be moved safely anymore.
A deviation can occur, for example, if the arm holding the tray gets moved while the robot is switched off.
To resolve the problem, it might be necessary to reconfigure the tray's reference position using the `MTS software`_.

---------------------------------
Using the manufacturer's software
---------------------------------

To recalibrate the tray using the manufacturer's software, you need the following items:

- Windows (10) Computer/Laptop with internet connection (for downloads)
- An esd `CAN-USB/2`_ device (confirmed working but `CAN-USB Mini`_ might also work):

  |canusb|

- Matching USB cable (probably type A <-> type B)

Download and install the following software:

- `CAN-USB/2 drivers`_ from esd (free account required)
- `CANopen tools`_ from esd (free account required)
- `MTS software`_ from Schunk

Follow these steps to recalibrate the tray:

#. Disconnect the tray's serial cable labelled ``tray`` from the grey USB adapter that is connected to the robot (see below)

   |tray-wiring|

#. Connect your computer to the serial cable using the `CAN-USB/2`_ device

#. From the CANopen tools run :command:`COT_ResetToSMP` and select the joint you want to move (see below)

   - Joint ``7``: power joint that lifts the tablet
   - Joint ``8``: power joint that rotates the tablet
   - Joint ``10``: shoulder joint

   |tray|

#. Run the :program:`MTS` software and select ``500,000`` Baudrate
#. Use move relative pose to move to the new reference point
#. Press the reference button to set zero position (new reference point)
#. Close the :program:`MTS` software
#. From the CANopen tools run :command:`SMP_ResetToCANopen` and select the same joint again
#. Plug back the tray's serial cable to peak USB box
#. Reboot the robot so the tray joints initialize to the new value

To see if you have calibrated everything correctly, start :ref:`cob3` as usual and check if the tray position is correct in :program:`RViz` after initialization in the dashboard.

.. #. Password: Schunk
