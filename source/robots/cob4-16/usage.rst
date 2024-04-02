.. _cob4_usage:

==============
Advanced usage
==============

.. todo::

  This page is a stub, fill it with content!

---------------
Useful commands
---------------

.. code-block::

  roslaunch uh_cob dashboard.launch

---------------
Modify defaults
---------------

.. warning::

  This section assumes that the default processes on the robot have been stopped, that the terminal's :ref:`environment` is set to ``cob4``, and that :ref:`ros_ip` is configured correctly.

If you need the control components to run with a different configuration, you can start them individually or with different parameters, for example, on a local computer.
The ``bringup.launch`` launch configuration supports arguments such as ``env`` that can be set to configure non-default locations other than the default ``robothouse2``, for example, special ones used in studies or demonstrations.
Besides the plain map, environments also set common navigation goals that can be used in interactive scenarios.
For a complete list of environments, please have a look at the `Robot House ROS packages <https://gitlab.com/robothouse/rh-user/uh_robot_cfg/-/tree/master/uh_environments/config/envs>`_.

.. code-block::

  $ roslaunch uh_cob bringup.launch env:=<environment>

If you only need navigation use the following command to start it individually.
Besides the ``env`` parameter, it also supports a ``map`` parameter that can be used to specify any other map:

.. code-block::

  $ roslaunch uh_cob navigation.launch env:=<environment> map:=<map>


----------
Navigation
----------

.. code-block::

  roslaunch uh_cob rviz.launch


Local navigation
================

Start cob_navigation_local navigation and RViZ:

.. code-block::

  roslaunch cob_navigation_local 2dnav_ros_dwa.launch robot:=cob4-3
  roslaunch cob_navigation_local rviz.launch


Record a new map
================

Start navigation:

.. code-block::

  roslaunch cob_navigation_slam 2dnav_ros_dwa.launch robot:=cob4


Visualize in RVIZ:

.. code-block::

  roslaunch cob_navigation_slam rviz.launch


Optional: Use keyboard to move robot

.. code-block::

  roslaunch cob_teleop teleop_keyboard.launch


Save map:

.. code-block::

  rosrun map_server map_saver -f <map_directory/map_name>


Use an existing map
===================

.. code-block::

  roslaunch cob_navigation_global 2dnav_ros_dwa.launch robot:=cob4 map:=/opt/robots/share/cob/map.yaml
  roslaunch cob_navigation_global rviz.launch

