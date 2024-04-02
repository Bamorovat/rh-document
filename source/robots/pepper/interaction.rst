.. _Choregraphe: http://doc.aldebaran.com/2-5/software/choregraphe/index.html
.. _unsplash: https://unsplash.com

.. _pepper_interaction:

=================
 Interactive demo
=================

We have programmed an interactive demonstration that can be used for showcasing visitors the interactive capabilities of :ref:`pepper` as well as Robot House functions and the interplay between them.

-----------------
Starting the demo
-----------------

To start the demonstration, you have to start the demo script on one of the pre-configured robot house computers.
Please follow :ref:`pepper_startup` to prepare the robot.

.. note::

  You can safely omit starting `Choregraphe`_ but it will not interfere in case you want to have it ready for other demonstrations, e.g. :ref:`pepper_apps`.
  
#. Setup your terminal's :ref:`robot_env` to :ref:`pepper` (and common robot house infrastructure) and set a :ref:`ros_ip`:

   .. code-block::

      $ robot_env common pepper
      $ ros_ip

#. Start the script:

   .. code-block::

      $ rosrun uh_pepper demo_interactive.py

   *If not awake,* :ref:`pepper` *will wake up and calibrate. Blue LEDs at the ears signal an active dialogue system.*

#. Use verbal commands to trigger behaviours, see below.

-----------------------
Interacting with Pepper
-----------------------

You can verbally interact with Pepper in an interactive demo that currently has the following functionalities:

- `Hello and goodbye`_
- Play a `Promotional video`_
- Execute a `Dancing routine`_
- Display `Photo albums`_
- `Face learning and recognition`_
- `Set a reminder`_
- Change its `Degree of interactivity`_

When Pepper is deployed in Robot House, it additionally has the following functions:

- Display the `Sensor map`_
- `Activity detection`_ reports
- `Device manipulation`_

The below sections explain how to trigger and use these functions in detail. First, they will present a general command structure that let's you start or stop
a certain routine. These commands usually contain some keywords, like ``command`` or ``reference`` which should be replaced by a list of words or phrases as indicated
in a table below the command. Commands also may contain optional words or phrases that might be left out when speaking, :dfn:`indicated like this`.

Often, the command structure looks like this, where the words *Pepper* and *please* are optional, followed by some command:

    :dfn:`Pepper` :dfn:`please` do something.

------------------------------
Functions available everywhere
------------------------------

Hello and goodbye
=================

This routine lets you start and end an interaction with Pepper where the robot will reply with a randomly selected greeting or farewell phrase.

**Command structure**:

    ``greeting`` :dfn:`Pepper`.

.. admonition:: Example Utterancess

    | Hello.
    | Good bye Pepper.

+-------------------------------------------------+---------------+
| ``greeting``                                    | Effect        |
+=================================================+===============+
| hello                                           | Pepper greets |
|                                                 | back          |
| how are you?                                    |               |
|                                                 |               |
| good morning                                    |               |
|                                                 |               |
| good afternoon                                  |               |
|                                                 |               |
| are you all right?                              |               |
|                                                 |               |
| what's up?                                      |               |
|                                                 |               |
| hi                                              |               |
|                                                 |               |
| hiya                                            |               |
|                                                 |               |
| hey                                             |               |
+-------------------------------------------------+---------------+
| good bye                                        | Pepper says   |
|                                                 | goodbye       |
| have a lovely evening                           |               |
|                                                 |               |
| see you later                                   |               |
|                                                 |               |
| take care                                       |               |
+-------------------------------------------------+---------------+

.. raw:: html

    <div class="yt">
        <iframe src="https://www.youtube.com/embed/9zdr0c0G_RU" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
    <br>


Promotional video
=================

Pepper can display a promotional video, by default a video of Robot House, when asked to do so. The video can be played, paused, restarted and stopped.

**Command structure**:

    :dfn:`Pepper` :dfn:`please` ``command`` :dfn:`the` ``reference``.

.. admonition:: Example Utterances

    | Pepper can I see the video.
    | Please show me Robot House.

+-------------------------------------------------+----------------------------------+
| ``command``                                     | Effect                           |
+=================================================+==================================+
| show                                            | (Re-)starts the video            |
|                                                 |                                  |
| show me                                         |                                  |
|                                                 |                                  |
| open                                            |                                  |
|                                                 |                                  |
| play                                            |                                  |
|                                                 |                                  |
| I want to see                                   |                                  |
|                                                 |                                  |
| I would like to see                             |                                  |
|                                                 |                                  |
| can I see                                       |                                  |
+-------------------------------------------------+----------------------------------+
| pause                                           | Pauses the video (stays visible) |
+-------------------------------------------------+----------------------------------+
| resume                                          | Resumes a paused video           |
+-------------------------------------------------+----------------------------------+
| stop                                            | Stops the video and hides it     |
|                                                 |                                  |
| hide                                            |                                  |
|                                                 |                                  |
| close                                           |                                  |
+-------------------------------------------------+----------------------------------+

+-------------------------+
| ``reference``           |
+=========================+
| video                   |
|                         |
| promotion video         |
|                         |
| project video           |
|                         |
| Robot House             |
+-------------------------+

.. note::

    The video can also be started or stopped by triggering the robot's ``back bumper`` with your foot and paused using its ``left bumper``.
    Moreover, all sound output can be muted with the robot's ``right bumper``.

.. raw:: html

    <div class="yt">
        <iframe src="https://www.youtube.com/embed/kk5fQFJA0yM" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
    <br>

Dancing routine
===============

With the dancing routine, Pepper can display some sequence where it plays the song *Greased Lightning* and performs some dance moves. A still image of the movie is shown on its screen.

**Command structure**:

    :dfn:`Pepper` :dfn:`please` ``command`` get active :dfn:`together`.

.. admonition:: Example Utterances

    Let's get active.

+-------------------------------------------------+----------------------------------+
| ``command``                                     | Effect                           |
+=================================================+==================================+
| I want to                                       | Starts dancing routine (Grease)  |
|                                                 |                                  |
| let's                                           |                                  |
+-------------------------------------------------+----------------------------------+

.. note::

    The behaviour can be stopped by triggering the robot's ``back bumper`` with your foot.
    Moreover, all sound output can be muted with the robot's ``right bumper``.
    
.. raw:: html

    <div class="yt">
        <iframe src="https://www.youtube.com/embed/YDkAQfRSkE8" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
    <br>

Photo albums
============

Using this routine, Pepper can display a curated list of photo albums from `unsplash`_. Currently available are albums about *travel*, *animals*, *nature*, and *arts & culture*.

**Command structure**:

    :dfn:`Pepper` :dfn:`please` ``command`` ``modifier`` * ``reference``.

`*modifier is optional and valid with display command only`

.. admonition:: Example Utterances

    | Show some photo albums.
    | I want to see other photos.

+-------------------------------------------------+----------------------------------+
| ``command``                                     | Effect                           |
+=================================================+==================================+
| show                                            | Displays a randomly selected     |
|                                                 | photo album                      |
| show me                                         |                                  |
|                                                 |                                  |
| open                                            |                                  |
|                                                 |                                  |
| display                                         |                                  |
|                                                 |                                  |
| I want to see                                   |                                  |
|                                                 |                                  |
| I would like to see                             |                                  |
|                                                 |                                  |
| can I see                                       |                                  |
+-------------------------------------------------+----------------------------------+
| hide                                            | Hide photo album                 |
|                                                 |                                  |
| close                                           |                                  |
|                                                 |                                  |
| stop showing                                    |                                  |
+-------------------------------------------------+----------------------------------+

+-------------------------+
| ``modifier``            |
+=========================+
| some                    |
|                         |
| more                    |
|                         |
| other                   |
+-------------------------+

+-------------------------+
| ``reference``           |
+=========================+
| photos                  |
|                         |
| images                  |
|                         |
| pictures                |
|                         |
| photo albums            |
+-------------------------+

Face learning and recognition
=============================

This routine makes use of Pepper's people perception apabilities. The robot can attempt to learn a face and associate it with a name that is typed in on its virtual keyboard.
It can also be asked to recognise a face and recall the associated name.

**Command structure**:

    :dfn:`Pepper` :dfn:`please` ``command`` ``reference``.

.. admonition:: Example Utterances

    | Please remember my name.
    | Recognise me.
    

+-------------------------------------------------+----------------------------------+
| ``command``                                     | Effect                           |
+=================================================+==================================+
| remember                                        | Start face learning routine      |
|                                                 |                                  |
| learn                                           |                                  |
+-------------------------------------------------+----------------------------------+
| forget                                          | Forget face currently seen       |
+-------------------------------------------------+----------------------------------+
| recognise                                       | List people in field of view     |
+-------------------------------------------------+----------------------------------+

+-------------------------+
| ``reference``           |
+=========================+
| my name                 |
|                         |
| my face                 |
|                         |
| me                      |
|                         |
| who I am                |
+-------------------------+

.. raw:: html

    <div class="yt">
        <iframe src="https://www.youtube.com/embed/0hGThy9rBN0" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
    <br>

.. raw:: html

    <div class="yt">
        <iframe src="https://www.youtube.com/embed/SVvflygL1iA" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
    <br>

Set a reminder
==============

This routine allows you to set a reminder to be triggered after a certain time (currently limited to *1*, *2*, *5*, *10*, *20* minutes). The topic or reason for the reminder can be
entered via a virtual keyboard on the robot's tablet.

**Command structure**:

    :dfn:`Pepper` :dfn:`please` ``command``.

.. admonition:: Example Utterances

    Pepper set a reminder.

+-------------------------------------------------+-----------------------------------+
| ``command``                                     | Effect                            |
+=================================================+===================================+
| set a reminder                                  | Start reminder routine asking     |
|                                                 | for duration and topic then       |
|                                                 | triggering reminder after timeout |
+-------------------------------------------------+-----------------------------------+


Degree of Interactivity
=======================

It is sometimes desirable to disable the interactive dialogue or Pepper's head movements, for exmaple when explaining to an audience or taking photos. This routine can temporarily disable and re-enable such functions.

**Command structure**:

    :dfn:`Pepper` :dfn:`please` ``command``.

.. admonition:: Example Utterances

    | Pepper stop listening.
    | Stop moving.

+-------------------------------------------------+----------------------------------+
| ``command``                                     | Effect                           |
+=================================================+==================================+
| start moving                                    | (Re-)start pepper attention      |
|                                                 | towards person                   |
| resume moving                                   |                                  |
+-------------------------------------------------+----------------------------------+
| stop moving                                     | Stop pepper attention            |
|                                                 | towards person and look straight |
| stand still                                     |                                  |
+-------------------------------------------------+----------------------------------+
| stop listening                                  | Stop pepper dialogue             |
|                                                 |                                  |
| stop talking                                    |                                  |
|                                                 |                                  |
| be quiet                                        |                                  |
|                                                 |                                  |
| ignore us                                       |                                  |
+-------------------------------------------------+----------------------------------+
| go to sleep                                     | Stop dialogue and                |
|                                                 | attention towards person,        |
|                                                 | go to resting posture            |
+-------------------------------------------------+----------------------------------+
| wake up                                         | (Re-)start dialogue and          |
|                                                 | attention towards person,        |
|                                                 | go to resting posture            |
+-------------------------------------------------+----------------------------------+

.. note::

    The dialogue can also be started or stopped by touching the robot's ``left hand``. Attention can be started or stopped by touching the robot's ``right hand``.
    Moreover, all sound output can be muted when triggering the robot's ``right bumper`` with your foot.

.. raw:: html

    <div class="yt">
        <iframe src="https://www.youtube.com/embed/7sHi84-Eaac" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
    <br>

.. raw:: html

    <div class="yt">
        <iframe src="https://www.youtube.com/embed/7bMIrLF5U20" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
    <br>

-----------------------------
Functions only in Robot House
-----------------------------


Sensor map
==========

When deployed in Robot House, Pepper can display the floor plan of the house with a live view of the smart home sensors overlayed.

**Command structure**:

    :dfn:`Pepper` :dfn:`please` ``command`` the ``reference``.

.. admonition:: Example Utterances

    | Hide the sensor map.
    | Please show the sensors.

+-------------------------------------------------+----------------------------------+
| ``command``                                     | Effect                           |
+=================================================+==================================+
| show                                            | Displays a website that contains |
|                                                 | the Robot House sensor map       |
| show me                                         |                                  |
|                                                 |                                  |
| open                                            |                                  |
|                                                 |                                  |
| display                                         |                                  |
|                                                 |                                  |
| I want to see                                   |                                  |
|                                                 |                                  |
| I would like to see                             |                                  |
|                                                 |                                  |
| can I see                                       |                                  |
+-------------------------------------------------+----------------------------------+
| hide                                            | Hide website with sensor map     |
|                                                 |                                  |
| close                                           |                                  |
|                                                 |                                  |
| stop showing                                    |                                  |
+-------------------------------------------------+----------------------------------+

+-------------------------+
| ``reference``           |
+=========================+
| map                     |
|                         |
| sensors                 |
|                         |
| sensor map              |
|                         |
| floor plan              |
+-------------------------+

.. raw:: html

    <div class="yt">
        <iframe src="https://www.youtube.com/embed/hNEFds_fT10" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
    <br>

.. _pepper_map_hide:

.. raw:: html

    <div class="yt">
        <iframe src="https://www.youtube.com/embed/YnZhb58YvR4" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
    <br>

Activity detection
==================

Pepper can report on various activities in Robot House using the smart sensor infrastructure, potentially devising some recommendations for actions like increasing the room temperature or taking a drink.

**Command structure**:

    :dfn:`Pepper` :dfn:`please` ``inform`` my ``report``.

.. admonition:: Example Utterances

    | Pepper summarise my activities today.
    | Tell me about my hydration.

+-------------------------------------------------+----------------------------------+
| ``inform``                                      | Effect                           |
+=================================================+==================================+
| summarise                                       | Generates a summary report       |
|                                                 | based on sensor readings         |
| tell me about                                   |                                  |
|                                                 |                                  |
| report                                          |                                  |
+-------------------------------------------------+----------------------------------+


+-------------------------+----------------------------------+
| ``report``              | Type                             |
+=========================+==================================+
| activities today        | bed, TV, room usage, etc.        |
+-------------------------+----------------------------------+
| hydration               | tap, fridge, kettle usage, etc.  |
|                         |                                  |
| hydration level         |                                  |
+-------------------------+----------------------------------+


Device manipulation
===================

You can use the following commands to manipulate certain devices (or device groups) in the house.

**Command structure for enabling a device:**

    :dfn:`Pepper` :dfn:`please` switch/turn on the ``device``.

**Command structure for disabling a device:**

    :dfn:`Pepper` :dfn:`please` switch/turn the ``device`` off.

.. admonition:: Example Utterances

    | Pepper switch on the kettle.
    | Please turn the coffee machine off.

+-------------------------------------------------+----------------------------------+
| ``device``                                      | Description                      |
+=================================================+==================================+
| light(s)                                        | Living room lights               |
+-------------------------------------------------+----------------------------------+
| kettle                                          | Kettle plug (kitchen)            |
+-------------------------------------------------+----------------------------------+
| coffee machine                                  | Coffee machine plug (kitchen)    |
+-------------------------------------------------+----------------------------------+

.. note::

    Individual commands are more flexible, see below.

+-------------------------------------------------+-----------------------------------+
| Individual commands                             | Description                       |
+=================================================+===================================+
| Prepare/make :dfn:`a/some` tea                  | Kettle plug (kitchen) on          |
|                                                 |                                   |
| Boil :dfn:`some` water                          |                                   |
+-------------------------------------------------+-----------------------------------+
| Stop the kettle/making tea                      | Kettle plug (kitchen) off         |
+-------------------------------------------------+-----------------------------------+
| Prepare/make :dfn:`a/some` coffee               | Coffee machine plug (kitchen) on  |
+-------------------------------------------------+-----------------------------------+
| Stop the kettle/making tea                      | Coffee machine plug (kitchen) off |
+-------------------------------------------------+-----------------------------------+
| Charge your friends/:dfn:`the/all` robots       | All robot charging plugs on       |
+-------------------------------------------------+-----------------------------------+
| Stop charging your friends/:dfn:`the/all` robots| All robot charging plugs off      |
+-------------------------------------------------+-----------------------------------+
| Increase the brightness/illumination.           | Increase brightness (living) 30%  |
+-------------------------------------------------+-----------------------------------+
| Decrease the brightness/illumination.           | Decrease brightness (living) 30%  |
+-------------------------------------------------+-----------------------------------+

.. raw:: html

    <div class="yt">
        <iframe src="https://www.youtube.com/embed/VuZjXbwwYG4" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
    <br>


.. raw:: html

    <div class="yt">
        <iframe src="https://www.youtube.com/embed/zqNSQyd3D-k" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
    <br>

.. raw:: html

    <div class="yt">
        <iframe src="https://www.youtube.com/embed/o3cFd--mWcg" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
    <br>

.. raw:: html

    <div class="yt">
        <iframe src="https://www.youtube.com/embed/kci4XkZsYnc" frameborder="0" allowfullscreen style="position: absolute; top: 0; left: 0; width: 100%; height: 100%;"></iframe>
    </div>
    <br>
