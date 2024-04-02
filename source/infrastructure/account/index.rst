.. _team: https://robothouse.herts.ac.uk/team/
.. _Generate an SSH key: https://www.ssh.com/ssh/keygen/

.. _ROS: https://www.ros.org/
.. _Kinetic: http://wiki.ros.org/kinetic/
.. _Sawyer Dependencies: https://sdk.rethinkrobotics.com/intera/Workstation_Setup
.. _Robot House ROS: https://gitlab.com/robothouse/rh-user/uh_robot_cfg/
.. _catkin: http://wiki.ros.org/catkin/
.. _CMakeLists.txt: http://wiki.ros.org/catkin/CMakeLists.txt

.. _account:




.. |br| raw:: html

   <br />

==============
 Account setup
==============

The Robot House :ref:`Robot House network <network>` includes a number of computers that you can use for conducting research.
This page guides you how to setup your account so that you can comfortably use the network and the pre-installed ROS distribution.

.. _ssh:

------------
Secure shell
------------

It is immensely useful to setup password-less SSH login for working with the computers in Robot House. A correct configuration will allow you to log into Robot House computers without typing a password (from internal and external devices). Moreover, it will also enable the following:

 * Shell access to the robots
 * Remote shell access to Robot House
 * Using ``roslaunch`` with the ``<machine>`` tag to start ROS nodes on other computers

Internal devices
================

Follow these steps to configure SSH for the computers in the :ref:`Robot House network <network>`.

#. To start, you first need to generate an SSH key pair (See also the official instructions to `Generate an SSH key`_):

   .. code-block::

      $ ssh-keygen
      Generating public/private rsa key pair.
      Enter file in which to save the key (/home/<user>/.ssh/id_rsa):
      Enter passphrase (empty for no passphrase):
      Enter same passphrase again:
      Your identification has been saved in /home/<user>/.ssh/id_rsa.
      Your public key has been saved in /home/<user>/.ssh/id_rsa.pub.
      The key fingerprint is:
      SHA256:1234567890XYZ <user>@<host>
      The key's randomart image is:
      +---[RSA 2048]----+
      |    .   .  ..oo..|
      |   . . .  . .o.X.|
      | F  . . o.  ..+ B|
      |   .   o.oo .+ ..|
      |    ..o.S   o..  |
      |   . %o=      .  |
      |    @.B... A   . |
      |   o.=. o. .    .|
      |    .oo  E. .    |
      +----[SHA256]-----+

   .. note:: Accept the default location for the key file by pressing enter once. Make sure to press enter two more times without typing in any passphrase if you want to avoid using passwords. SSH keys without passphrases are generally considered acceptable.

#. Then, tell SSH to accept this key for authentication when logging in from other computers:

   .. code-block::

      $ cp ~/.ssh/id_rsa.pub ~/.ssh/authorized_keys

#. The files that we have generated (``authorized_keys`` and the key pair) have to be distributed
   to all computers in the Robot House network. Paste the following into your terminal to copy them:

   .. code-block::

      $ for host in $RH_HOSTS;
      > do
      >   if [ ! $host == $HOSTNAME ];
      >   then
      >    scp ~/.ssh/id_rsa* ~/.ssh/authorized_keys $host:.ssh/;
      >   fi
      > done

   .. note:: There will be some output for copying the files but you will also have to type your password for each host and confirm each of the host's signatures with ``yes`` when prompted with the following:

      .. code-block::

        The authenticity of host '<host> (<ip>)' can't be established.
        ECDSA key fingerprint is SHA256:1234567890XYZ.
        Are you sure you want to continue connecting (yes/no)?

#. Finally, also distribute the ``known_hosts`` file to avoid accepting the signature on every host individually:

   .. code-block::

      $ for host in $RH_HOSTS;
      > do
      >   if [ ! $host == $HOSTNAME ];
      >   then
      >     scp ~/.ssh/known_hosts $host:.ssh/;
      >   fi
      > done

You can now use SSH to log into any host in Robot House without needing to type your password.

External devices
================

If you want to have access from your personal computer or laptop, you need to create a key pair with ``ssh-keygen`` on that device, too. You need to bring the key file to Robot House, either on a device that is connected to the Robot House network or on a USB stick.

#. For doing so, you first have to copy the public key file from your device to one of the computers in Robot House. Proceed according to the location of the key file:

   A) If you want to use the standard key **on your device**, enter the following to copy it to the correct location:

      .. code-block::

          $ scp ~/.ssh/id_rsa.pub <user>@<computer>:.ssh/id_rsa.personal.pub

      .. note:: Use your Robot House username and the name of a computer in Robot House that you have access to.

   B) If it is on **a USB stick**, plug it into a computer and copy the file to the correct location:

      .. code-block::

          $ cp /run/media/<user>/<USB-STICK>/id_rsa.pub ~/.ssh/id_rsa.personal.pub

      .. note:: Use your Robot House username and the name of the USB stick that you plugged in.

#. You then need to add the key as acceptable for authentication on all the computers in Robot House. Please log into **the computer that you have copied the file to** and issue the following command to add the key as valid for authentication:

   .. code-block::

      $ for host in $RH_HOSTS;
      > do
      >   ssh-copy-id -i ~/.ssh/id_rsa.personal.pub $host;
      > done


.. _password:

--------
Password
--------

.. note:: The second command (``robot_hosts``) will open a parallel connection to all of the computers using SSH at the same time.
          It may be a good idea to maximize the terminal window as you will be typing in all of the sub-windows simultaneously.

After you have setup SSH successfully, make sure to change your password on all the computers in Robot House.
When prompted, first enter your old password (given to you by one of the `team`_ members) followed by your new password (twice).

   .. code-block::

      $ robot_env common
      $ robot_hosts
      $ passwd
      Changing password for <user>.
      (current) UNIX password:
      Enter new UNIX password:
      Retype new UNIX password:
      passwd: password updated successfully


.. _ros_catkin:

--------------
ROS and catkin
--------------


The **Robot Operating System** (`ROS`_) is a set of software libraries and tools that help you build robot applications. It is released in distributions that are akin Linux distributions (e.g. Ubuntu) providing a collection of software to operate robots and other devices. Kinetic Kame (short: `Kinetic`_) is the primary distribution in use at Robot House as it is compatible with most of our hardware.

Common packages that are available on all computers in Robot House are:
 * A meta-package that contains a collection of packages for using ROS on a desktop computer: |br|
   ``ros-kinetic-desktop-full``
 * A meta-package for operating :ref:`cob4`: |br|
   ``ros-kinetic-care-o-bot-desktop``
 * A meta-package for operating and simulating :ref:`turtlebot2`: |br|
   ``ros-kinetic-turtlebot``, ``ros-kinetic-turtlebot-simulator``
 * Packages for operating and visualizing :ref:`pepper`: |br|
   ``ros-kinetic-pepper-robot``, ``ros-kinetic-pepper-meshes``
 * Various packages for operating :ref:`sawyer` (cf. `Sawyer Dependencies`_).

.. note:: For compatibility reasons, :ref:`fetch` packages are not installed as part of the base system but from source when loading its :ref:`robot_env`.


.. I didn't install these by hand, need to double check!
..    C) **ros-kinetic-husky-desktop** - Metapackage for Clearpath Husky visualization software.
..    D) **ros-kinetic-pr2-desktop** - A metapackage to aggregate several packages.
..    E) **ros-kinetic-kobuki-desktop** - Visualisation and simulation tools for Kobuki - Turtlebot2 Package

Besides official ROS packages, we provide our own packages (`Robot House ROS`_), which is loaded by default (see below). It contains:
 * Components to operate and visualize the sensory infrastructure of Robot House: |br|
   ``uh_core``, ``uh_webui``
 * Configuration files, custom startup and demo scripts, and utilities to operate robots: |br|
   ``uh_cob``, ``uh_fetch``, ``uh_pepper``, etc.
 * Environment configuration for different Robot House layouts and other places, e.g. the lab in E-125, including navigation maps: |br|
   ``uh_environments``

A `catkin`_ **workspace** is a folder where you modify, build, and install ROS packages. In case you want to write your own code to operate a robot, should use your own personal catkin workspace. For creating a workspace, follow these steps in the terminal of any Robot House computer:

    .. code-block::

        $ cd ~
        $ mkdir -p <your_catkin>_ws/src
        $ cd ~/<your_catkin>_ws/
        $ catkin_make

Every time when want to work with your workspace, i.e. when you open a new terminal, you need to source your now existing ``setup.bash`` file to load your workspace:

    .. code-block::

        $ source ~/<your_catkin>_ws/devel/setup.bash

.. note:: If you are going to use the Robots or Robot House environment setting, you need to add ``uh_core`` and ``uh_environments`` packages in the ``find_package (catkin REQUIRED COMPONENTS)`` section of the package's `CMakeLists.txt`_.

You can load multiple catkin workspaces at once and this provides you with access to all of the packages. Workspaces are extended hierarchically and, in fact, your personal catkin workspace already extends the system's ROS installation. When extending an existing workspace, individual files and scripts of existing packages will be replaced by a custom version if you use the same package and files names.

On the Robot House computers, there are different workspaces available which you can use based on your needs. Some workspaces are loaded automatically when opening a terminal window on one of the Robot House computers providing you access to its packages. In order of loading, these are:

    #. The default ROS installation in ``/opt/ros/kinetic``.
    #. The `Robot House ROS`_ installation and a few extra packages are loaded by the ``common`` :ref:`robot_env` in ``/opt/robots/common/``.

.. note:: If you want to alter the automatic loading of packages, edit the file ``~/.bashrc``, commenting out the appropriate lines. To do this on all Robot House computers, the command ``robot_hosts`` is recommended.

You can load other existing workspaces using the :ref:`robot_env` command for each robot individually. If you happen to name your workspace ``/home/<user>/<robot>_ws``, you can use ``robot_env --overlay <robot>`` to load your personal overlay to the workspace of ``<robot>`` using a single command. You can optionally load the workspaces manually by calling ``source /opt/robots/<robot>/setup.bash`` or source any other custom workspaces, for example, from your home folder.


For example, if you wanted to use your own packages that are in ``/home/<user>/<your_catkin_ws>/`` with the :ref:`fetch` robot, you need source your personal workspace after loading the robot environment:

    .. code-block::

        $ robot_env fetch
        $ source /home/<user>/<your_catkin_ws>/devel/setup.bash

You will now have access to the global installation of `ROS`_ kinetic, `Robot House ROS`_ packages, Robot House :ref:`fetch` packages, and your own packages in ``/home/<user>/<your_catkin_ws>/``. Alternatively, if you named your workspace ``/home/<user>/fetch_ws``, you can use a single command:

    .. code-block::

        $ robot_env --overlay fetch



.. What ROS distro? kinetic -- Done

.. What packages are available by default? -- Done
..
.. <<<<<<< HEAD
.. * uh_robot_cfg
.. * desktop-full
.. * robot packages (need to look at ros website for exact names probably). -- Done
.. =======
.. * desktop-full (ros-kinetic-desktop-full)
.. * robot packages (need to look at ros website for exact names probably).
     ros-kinetic-care-o-bot, etc.
.. * uh_robot_cfg (https://gitlab.com/robothouse/rh-user/uh_robot_cfg)
.. >>>>>>> 9db36a6937f217b304cd0fd4a7168578433706f4
..
.. What are workspaces for? - add custom packages -- Done
.. How to create a custom workspace and run catkin_make? (quick commands and add link to ros documentation as well) -- Done
..
.. Overlays in the following order: -- Done
..
.. #. defaults: /opt/ros/kinetic
.. #. defaults: robot_env common (this is an overlay to /opt/ros/kinetic)
.. #. optional: robot_env <robot> (this is an overlay to the common env, so it has /opt/ros/kinetic + the common workspace + the robot workspace)
.. #. optional: /home/<user>/<robot>_ws (when using robot_env --overlay this is a personal overlay to the <robot> workspace, so also all the others)
.. #. optional: source any other custom workspace


