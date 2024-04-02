.. _Robot House ROS: https://gitlab.com/robothouse/rh-user/uh_robot_cfg/-/tree/master/uh_core/src/uh_core
.. _gscam: http://wiki.ros.org/gscam
.. _openni2: http://wiki.ros.org/openni2_launch

.. _sensors:

===================
 Sensory technology
===================

Robot House is equipped with the current state-of-the art sensory technology to enhance the Robot House robots' perception capabilities.
Currently, there are more than 60 smart home sensors, two omnidirectional ceiling cameras and some portable RGB(-D) cameras.
On these pages, you can find information on how to employ them into your experiment, and how to troubleshoot in cases of known problems.

.. _ambient:

---------------
Ambient Sensors
---------------

.. _figmap:

.. figure:: /images/facility/map.png
   :figwidth: 40%
   :width: 100%
   :align: right
   :alt: Overview of Robot House sensors

   Overview of Robot House sensors

:numref:`figmap` shows an overview of the ambient sensors that are distributed over Robot House:

* Brightness, movement, and temperature sensors in every room
* Power consumption and plug status using switchable power plugs at almost every appliance, computer, standard lamp, and robot charger
* Lamp status and switchable lights in the living room
* Status sensor at every door, drawer, wardrobe, cupboard, and toilet seat lid
* Pressure mats on the sofas and in the bed
* Temperature and water flow sensors in the kitchen taps

Some of the sensors have a power switch that you need to enable if you want to use them:

   * Sofa pressure mats: At the top left of the sofa.
   * Kitchen cabinet and drawer sensors: In the lower corner cabinet to the left of the sink.
   * Living room cabinet and drawer sensors: Between the small and large cupboard.
   * Bedroom wardrobe door sensors: On top of the wardrobe.
   * Bedroom desk door sensors: On the left side of the desk.

.. note:: Wait one or two minutes for the sensors to connect. Sensors will be picked up by the sensor component.

The sensors will automatically publish state changes via ROS at ``/robothouse/sensors`` and can be actuated via ``/robothouse/actuators`` in the ``common`` :ref:`robot_env` where the :ref:`components` are active by default.
You can also address the sensors using ``sensors.py`` in the `Robot House ROS`_ interface.

.. note:: Please refer to :ref:`sensors_troubleshoot` in case the sensors are not working as expected or to :ref:`sensors_advanced` if you need a non-default setup.

.. _cameras:

-------
Cameras
-------

There are two omnidirectional cameras in the living room that cover the main experimentation area including the living room, corridor and parts of the kitchen. We also have a couple of RGB-D cameras that have a standard location but can be moved on a per-experiment basis. These usually cover the kitchen and two living room areas from a high angle shot.

.. note:: As the cameras are mobile equipment please ensure that they are plugged into the (correct) computers, see :ref:`network`.

All cameras will publish state changes on demand via ROS at various topics depending on their standard location, for example, ``/omni_livingroom`` or ``/rgbd_kitchen``. Please refer to :ref:`components` for details.

.. note:: Please refer to :ref:`sensors_troubleshoot` in case the cameras are not working as expected or if you need a non-default setup.

.. _components:

-----------------
Sensor Components
-----------------

There is a main ``bringup`` component within the `Robot House ROS`_ software that is permanently active on the host :term:`shakuras`, running as the user :term:`demo`. Besides providing other services, this component enables the use of both :ref:`ambient` and :ref:`cameras` on all computers in Robot House in the :ref:`robot_env` ``common``. When the ``bringup`` component is active, the following topics are active:

+---------------------+---------------------------+------+------------------------------+--------------------+
| Component           | Topic                     | Type | Data                         | Driver             |
+=====================+===========================+======+==============================+====================+
| Sensor interface    | ``/robothouse/sensors``   | Pub  | ``uh_core/SensorData``       | `Robot House ROS`_ |
+---------------------+---------------------------+------+------------------------------+--------------------+
| Actuator interface  | ``/robothouse/actuators`` | Sub  | ``uh_core/ActuatorData``     | `Robot House ROS`_ |
+---------------------+---------------------------+------+------------------------------+--------------------+
| RGB-D living room   | ``/rgbd_livingroom/[..]`` | Pub  | ``sensor_msgs/Image`` etc.   | `openni2`_         |
+---------------------+---------------------------+------+------------------------------+--------------------+
| RGB-D kitchen       | ``/rgbd_kitchen/[..]``    | Pub  | ``sensor_msgs/Image`` etc.   | `openni2`_         |
+---------------------+---------------------------+------+------------------------------+--------------------+
| RGB-D sofa area     | ``/rgbd_sofa/[..]``       | Pub  | ``sensor_msgs/Image`` etc.   | `openni2`_         |
+---------------------+---------------------------+------+------------------------------+--------------------+
| Omnicam living room | ``/omni_livingroom/[..]`` | Pub  | ``sensor_msgs/Image`` etc.   | `gscam`_           |
+---------------------+---------------------------+------+------------------------------+--------------------+
| Omnicam corridor    | ``/omni_corridor/[..]``   | Pub  | ``sensor_msgs/Image`` etc.   | `gscam`_           |
+---------------------+---------------------------+------+------------------------------+--------------------+

The following parts describe how to start and stop the ``bringup`` component, how to check whether the different sensors are functional, and how to configure more advanced use cases, such as only starting individual sensor components or running them in a different :ref:`robot_env`.

.. _sensors_startup:

Starting up
===========

Usually, the all components that makes the sensors available in ROS should already be running in the background at all times wrapped in a ``bringup`` component.
A possible exception from this default is, for example, when a :ref:`custom setup is active <sensors_advanced>` and the :ref:`component has been stopped <sensors_shutdown>`.
To restart the default components in such cases, follow these instructions:

.. warning:: If you started any of the components in ``bringup`` :ref:`manually <sensors_advanced>`, the according processes will be terminated.

#. Log into :term:`shakuras` as the :term:`demo` user:

   .. code-block::

      $ ssh demo@shakuras

#. Start a ``screen`` session to allow the components to run detached in the background:

   .. code-block::

      $ screen

#. Start the ``bringup`` component:

   .. code-block::

      $ roslaunch uh_core bringup.launch --screen


#. Press :kbd:`Ctrl + A,D` to detach the screen session and let the component run in the background.

.. _sensors_shutdown:

Shutting down
=============

If you want to use a more advanced setup, for example, if some of the ``bringup`` components interfere with your setup or if you need to have them active in another :ref:`robot_env`, you need to first stop the ``bringup`` component that is running by default.
Follow these instructions to do so:

#. At first, log into :term:`shakuras` as the :term:`demo` user where the components are usually active:

   .. code-block::

      $ ssh demo@shakuras

#. Attach the ``screen`` session where the components should be running:

   .. code-block::

      $ screen -r

#. Press :kbd:`Ctrl + C` to abort the process and wait for its termination.

.. note:: After you are finished with your work, please restart the default component following the instructions in :ref:`sensors_startup`.

.. _sensors_troubleshoot:

Troubleshoot
============

You can check whether the sensor component is running in the default configuration using the following instructions:

#. Set the :ref:`robot_env` to  ``common``:

   .. code-block::

      $ robot_env common

   .. note:: Specify any other environment if you want to see whether the components are running there, for example when you :ref:`manually started <sensors_startup>` the component in a custom configuration.

#. Check whether the necessary components are already active.

   A) If you need the :ref:`ambient`, check if they are up:

      .. code-block::

          $ rostopic list | grep robothouse
          /robothouse/actuators
          /robothouse/sensors

   B) Likewise, you can check whether the :ref:`cameras` are already active:

      .. code-block::

          $ rostopic list | grep cam
          /omni_livingroom/camera_info
          /omni_stairway/camera_info
          /rgbd_kitchen/depth/camera_info
          ...
          /rgbd_livingroom/depth/camera_info
          ...

In the above examples, the sensors and cameras are already active in the ``common`` :ref:`environment <environment>` and you do **not** need start them if you want to continue to use this environment.

.. note:: If the output is either empty or contains ``ERROR: Unable to communicate with master!`` the sensory components are not active and you may need to :ref:`start <sensors_startup>` them.


.. _sensors_advanced:

Advanced usage
==============

If the main ``bringup`` component is interfering with your setup or if you want to use the sensors in a specific :ref:`robot_env`, you need to start them individually. You can follow these steps on any computer in the Robot House :ref:`network <network>`.

.. warning:: Make sure that the components are not :ref:`already running <sensors_troubleshoot>` as some processes may get killed. Please :ref:`stop the defaults <sensors_shutdown>` if necessary.

#. Configure the :ref:`robot_env` to your needs:

   .. code-block::

      $ robot_env <robot>

#. Start one of the following components:

  A) Use the core ``bringup`` component to initialize **all services** including :ref:`ambient` and :ref:`cameras`:

     .. code-block::

        $  roslaunch uh_core bringup.launch

  B) **Only ambient sensors** without cameras

     .. code-block::

        $  roslaunch uh_core sensors.launch

  C) **Only cameras** without ambient sensors

     .. code-block::

        $  roslaunch uh_core cameras.launch

  .. note:: If the ``roslaunch`` command fails with ``ERROR: unable to contact ROS master at [http://<host>:11311]``, make sure that a ``roscore`` is running on the host that that you configure with the ``$ROS_MASTER_URI`` variable. This might happen, for example, if you use the :ref:`robot_env` ``common`` on a different computer than :term:`shakuras` as the command sets ``ROS_MASTER_URI=http://shakuras:11311`` .
