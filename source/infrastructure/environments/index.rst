.. _team: https://robothouse.herts.ac.uk/team/

.. _environment:

==========================
 Environment configuration
==========================

If you intend to use the :ref:`sensors` or one of the :ref:`robots`, you probably want to configure your shell environment accordingly.
We have implemented a number of convenience functions that are managed in the Robot House environment configuration project (`rh-env <https://gitlab.com/robothouse/rh-user/rh-env>`_).
Please feel free to contribute.

.. _robot_env:

-----------------
Robot environment
-----------------

The function ``robot_env`` allows you to set relevant environment and ROS workspace for each robot individually.
After calling the function, the current environment will be displayed using coloured letters in the command prompt of your terminal.
The following variables might be set depending on the environment you specify:

* ``$ROS_PACKAGE_PATH``
* ``$ROS_MASTER_URI``
* ``$ROBOT``
* ``$ROBOT_ENV``
* ...

Set up the environment using the following command:

.. code-block::

  $ robot_env [-h|--help] [-l|--local] [-o|--overlay] [ROBOT ...]
    Print and set robot environments

    Options:
     -h | --help:    Print this help text
     -l | --local:   Set ROS_MASTER_URI to http://localhost:11311
     -o | --overlay: Use the workspace at ~/$ROBOT_ws as a personal overlay

    Arguments:
     ROBOT:        A valid robot configuration.

The ``ROBOT`` argument thereby denotes the robot that you want to use. You can find the relevant argument in their respective documentation page.
Typing ``robot_env`` without any parameters also gives you a list of all currently supported robots.
If you use the ``--local`` option, the command set the ``$ROS_MASTER_URI`` variable to ``https://localhost:11311`` to allow working without the robot, for example in simulation contexts.
When the ``--overlay`` option is present the command uses a workspace in your home directory as an overlay.
An error will be displayed if ``--overlay`` is given but there is no workspace in the folder ``$HOME/$ROBOT_ws/`` or if the workspace is not correctly configured.

For example, to configure your environment to work with fetch and use your own catkin workspace as an overlay, type in the following:

.. code-block::

  $ robot_env -o fetch
  Loading robot space from /opt/robots/fetch/setup.bash
  Loading personal robot overlay from /home/<user>/fetch_ws/devel/setup.bash
  Loading environment from /opt/robots/etc/fetch.sh

.. note:: You can specify multiple robots with the ``robot_env`` where variables are potentially overridden by robots that are given later in the argument list.

A special robot configuration ``common``, which is usually available, configures a ROS workspace that is shared between all robots (and for example contains the Robot House ROS packages (`uh_robot_cfg <https://gitlab.com/robothouse/rh-user/uh_robot_cfg>`_). With this configuration, the ROS master is set to :term:`shakuras`.

.. note:: The environment is automatically set to ``common`` on every new `account <account>`_ and also if you logged in as the :term:`demo` user.


.. _ros_ip:

------
ROS IP
------

A special variable, ``$ROS_IP``, needs to be set correctly in some use cases.
We provide the function ``ros_ip`` to set this variable semi-automatically.

.. code-block::

  $ ros_ip [-h|--help] [-l|--list] [DEVICE]
    Determine and set ROS_IP variable

    Options:
     -h | --help: Print this help text
     -l | --list: List network devices

    Arguments:
     DEVICE:      Set ROS_IP to a the IP address of a specific device.
                  If empty the first non loopback device will be used.

If you call the function without parameters, it will try to determine the correct address by itself:

.. code-block::

   $ ros_ip
   Setting ROS_IP to xx.x.x.xxx (default device: enp0s31f6)

.. note:: If the computer is equipped with more than one network device, the command will present you with the alternative device names.

You can also call the function with the device name as a parameter to set the correct address for this device:

.. code-block::

  $ ros_ip docker0
  Setting ROS_IP to xx.x.x.xxx (specific device: docker0)
