.. _MoveIt: https://moveit.ros.org/

.. _fetch_usage:

==============
Advanced usage
==============

This section highlights some non-standard scenarios that might occur when environments change, for example when new furniture is introduced or the robot is brought to a new place.

-------------
Stop defaults
-------------

Among others, navigation and arm control (`MoveIt`_) are both started automatically on the robot, see :ref:`fetch_startup`.
In some advanced use cases, these processes might interfere with what you need the robot to do and you may have to log into the robot and stop these processes.

.. warning:: Please mind that this also stops other processes like the :ref:`fetch_remote` demonstrations.
             Only follow these instructions if you know what you are doing!

.. code-block::

  $ ssh fetch42
  $ screen -r

Press :kbd:`Ctrl+C` to abort the running process (``roslaunch uh_fetch bringup.launch``). If you change your mind, press :kbd:`Ctrl+A,D` to detach the screen session.

---------------
Modify defaults
---------------

.. warning::

  This section assumes that the default processes on the robot have been stopped, that the terminal's :ref:`environment` is set to ``fetch``, and that :ref:`ros_ip` is configured correctly.

If you need the control components to run with a different configuration, you can start them individually or with different parameters, for example, on a local computer.
The ``bringup.launch`` launch configuration supports arguments such as ``env`` that can be set to configure non-default locations other than the default ``robothouse2``, for example ``e125``, or ``forum``.
Besides the plain map, environments also set common navigation goals that can be used in interactive scenarios.
For a complete list of environments and maps, please have a look at the `Robot House ROS packages <https://gitlab.com/robothouse/rh-user/uh_robot_cfg/-/tree/master/uh_environments/config/envs>`_.

.. code-block::

  $ roslaunch uh_fetch bringup.launch env:=<environment>

If you only need navigation use the following command to start it individually.
Besides the ``env`` paramter, it also supports a ``map`` parameter that can be used to specify any other map:

.. code-block::

  $ roslaunch uh_fetch navigation.launch env:=<environment> map:=<map>
  
For example, if you have brought the robot to the lab in E125 and want to use a custom map ``mymap`` that you have recorded last-minute (see below), type in the following:

.. code-block::

  $ roslaunch uh_fetch navigation.launch env:=e125 map:=./mymap.yaml

To only start a component for controlling the arm, please use :ref:`fetch`'s built-in `MoveIt`_ configuration:

.. code-block::

  $ roslaunch fetch_moveit_config move_group.launch

----------------
Record a new map
----------------

.. warning::

  This section assumes that the default processes on the robot have been stopped, that the terminal's :ref:`environment` is set to ``fetch``, and that :ref:`ros_ip` is configured correctly.

If you need to record a map of the environment you can use the following instructions.
Firstly, start a local navigation component to build up a map.
If you don't have :program:`RViz` running, start it to inspect the results.

.. note:: The map's origin will be at the robot's current position.

.. code-block::

  $ roslaunch fetch_navigation build_map.launch
  $ roslaunch uh_fetch rviz.launch

Carefully drive the robot around using the :ref:`fetch_remote` control until you are satisfied with the result.
Do not move the robot too quickly or rotate it unnecessarily to achieve a better map quality.
The ``map_saver`` module can be used to store the map as two files that belong together: an image and a metadata description file.

.. code-block::

  $ rosrun map_server map_saver -f <map_directory/map_name>
  
For example, type in the following to generate the files ``mymap.yaml`` and ``mymap.png`` in the current directory:

.. code-block::

  $ rosrun map_server map_saver -f ./mymap


----------
Simulation
----------

#. Setup your terminal's :ref:`environment` to use the ``fetch`` software but not relying on the robot for ROS but instead on the local computer:

  .. code-block::

    $ robot_env -l fetch

#. Start the robot simulation:

  .. todo:: Give more elaborate information on these examples, in the future the simulation section might become a dedicated page.

  .. code-block::

    $ roslaunch fetch_gazebo_demo demo.launch
    $ roslaunch fetch_gazebo playground.launch
    $ roslaunch fetch_moveit_config demo.launch

