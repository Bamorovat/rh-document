.. _standard remote control functions: http://docs.fetchrobotics.com/teleop.html

.. _fetch_remote:

===============
 Remote control
===============

.. _fig_fetch_remote_front:

.. figure:: /images/fetch/remote1.png
   :figwidth: 50%
   :width: 100%
   :align: right
   :alt: Fetch remote control (main buttons)

   Fetch remote control (main buttons)

.. _fig_fetch_remote_top:

.. figure:: /images/fetch/remote2.png
   :figwidth: 50%
   :width: 100%
   :align: right
   :alt: Fetch remote control (shoulder buttons)

   Fetch remote control (shoulder buttons)

Besides offering `standard remote control functions`_ for :ref:`fetch`, we have modified the robot's remote control so that it can be used to trigger a number of pre-programmed demonstrations. For this to work, the robot's bringup module has to be active, which is usually done *automatically* when :ref:`fetch_startup` the robot.

Any of the buttons described below (depicted in :numref:`fig_fetch_remote_front`) will trigger a demonstration if pressed together with the so-called *dead man* switch. The dead man switch for our custom demonstrations and behaviours is ``upper left shoulder`` (button ``10`` in :numref:`fig_fetch_remote_top`).

.. note:: The dead man switch is *the same* as the one for `standard remote control functions`_. It is in the same position as the one that triggers demonstrations on the :ref:`cob4_remote` for :ref:`cob4`.

If the same combination is pressed again, the currently active behaviour will be canceled and the robot is put back into a safe default position. Physical behaviours involving robot movements cannot be run in parallel and therefore will not be triggered if such a behaviour is already active. Other behaviours might run in parallel although for example individual utterances might get delayed.

----------------------------
Overview of button functions
----------------------------

+-----------------------------+----------------------------------------------------------+
| Button                      | Behaviour                                                |
+=============================+==========================================================+
| Square ``15``               | :ref:`Increase living room brightness <cob4_brightness>` |
+-----------------------------+----------------------------------------------------------+
| Circle ``13``               | :ref:`Decrease living room brightness <cob4_brightness>` |
+-----------------------------+----------------------------------------------------------+
| Upper right shoulder ``11`` | Send ``OK`` message to ROS                               |
+-----------------------------+----------------------------------------------------------+
| Lower right shoulder ``9``  | Send ``Cancel`` message to ROS                           |
+-----------------------------+----------------------------------------------------------+

.. todo:: Explain messages.

+-------------+----------------------+
| Button      | Phyisical Behaviour  |
+=============+======================+
| Left ``7``  | :ref:`fetch_pose`    |
+-------------+----------------------+
| Right ``5`` | :ref:`fetch_pickup`  |
+-------------+----------------------+

----------------
Behaviour videos
----------------

.. _fetch_pose:

Exemplary pickup poses
======================

.. raw:: html

    <div class="yt">
        <iframe src="https://www.youtube.com/embed/Nr5wC4ggNyo" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
    <br>

.. _fetch_pickup:

Find & pick an object and place it on the table
===============================================

.. raw:: html

    <div class="yt">
        <iframe src="https://www.youtube.com/embed/4-Kf-vcEcEY" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
    <br>

