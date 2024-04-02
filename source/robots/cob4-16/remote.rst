.. _standard remote control functions: http://wiki.ros.org/Robots/cob4/manual/operation#Remote_control

.. _cob4_remote:

===============
 Remote control
===============

.. _fig_cob4_remote:

.. figure:: /images/cob4-16/remote.jpg
   :figwidth: 40%
   :width: 100%
   :align: right
   :alt: Care-o-bot 4 remote control

   Care-o-bot 4 remote control

Besides offering `standard remote control functions`_ for :ref:`cob4`, we have modified its remote control (depicted in  :numref:`fig_cob4_remote`) so that it can be used to trigger a number of pre-programmed demonstrations. For this to work, the robot's bringup module has to be active, which is usually a part of :ref:`cob4_startup`:

.. code-block::

  $ roslaunch uh_cob bringup.launch

Any of the following buttons, if pressed together with the so-called dead man switch, will trigger a demonstration. The dead man switch for our custom demonstrations and behaviours is ``upper left shoulder``.

.. note:: The dead man switch is *different* from the one that enables `standard remote control functions`_. It is in the same position as the dead man switch on the :ref:`fetch_remote` for :ref:`fetch`.

If the same combination is pressed again, the currently active behaviour will be cancelled and the robot is put back into a safe default position. Physical behaviours involving robot movements cannot be run in parallel and therefore will not be triggered if such a behaviour is already active. Other behaviours might run in parallel although for example individual utterances might get delayed.

----------------------------
Overview of button functions
----------------------------

+--------+----------------------------------------------------------+
| Button | Behaviour                                                |
+========+==========================================================+
| A      | :ref:`Increase living room brightness <cob4_brightness>` |
+--------+----------------------------------------------------------+
| B      | :ref:`cob4_monitor`                                      |
+--------+----------------------------------------------------------+
| X      | :ref:`cob4_battery`                                      |
+--------+----------------------------------------------------------+
| Y      | :ref:`Decrease living room brightness <cob4_brightness>` |
+--------+----------------------------------------------------------+

+--------+-----------------------------+
| Button | Phyisical Behaviour         |
+========+=============================+
| Up     | :ref:`cob4_welcome`         |
+--------+-----------------------------+
| Down   | :ref:`cob4_parking`         |
+--------+-----------------------------+
| Left   | :ref:`cob4_handover`        |
+--------+-----------------------------+
| Right  | Demonstrate arm movements   |
+--------+-----------------------------+

----------------
Behaviour videos
----------------

.. _cob4_brightness:

Alter living room brightness
============================

.. raw:: html

    <div class="yt">
        <iframe src="https://www.youtube.com/embed/Ix0vWOeIc1g" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
    <br>

.. _cob4_monitor:

Monitor robot house sensors
===========================

.. raw:: html

    <div class="yt">
        <iframe src="https://www.youtube.com/embed/0I8tXK6qQKM" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
    <br>

.. raw:: html

      <div class="yt">
          <iframe src="https://www.youtube.com/embed/LFQQlw_eTAU" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
      </div>
      <br>

.. _cob4_battery:

Give battery information
========================

.. raw:: html

    <div class="yt">
        <iframe src="https://www.youtube.com/embed/N1mwizG1kQE" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
    <br>

.. _cob4_welcome:

Welcome greeting and waving
===========================

.. raw:: html

    <div class="yt">
        <iframe src="https://www.youtube.com/embed/_PnYfqJf37I" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
    <br>

.. _cob4_parking:

Go to parking position
======================

.. raw:: html

    <div class="yt">
        <iframe src="https://www.youtube.com/embed/y0Ii1MuO5lI" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
    <br>

.. _cob4_handover:

Handover demonstration
======================

.. raw:: html

    <div class="yt">
        <iframe src="https://www.youtube.com/embed/fVJHj4TUxPs" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
    <br>
