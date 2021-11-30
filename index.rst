.. title:: ThycoticCentrify - Privilige Manager Handson Training

.. toctree::
   :maxdepth: 2
   :caption: Module 1
   :name: _m1
   :hidden:

   module1/module1

.. toctree::
  :maxdepth: 2
  :caption: Module 2 - Basic Configuration
  :name: _m2
  :hidden:


.. toctree::
  :maxdepth: 2
  :caption: Module 3 - Users, Groups and Roles
  :name: _m3
  :hidden:


.. toctree::
  :maxdepth: 2
  :caption: Module 4 - Folder and Policies
  :name: _m4
  :hidden:


.. toctree::
  :maxdepth: 2
  :caption: Module 5 - Secret Templates
  :name: _m5
  :hidden:


.. toctree::
  :maxdepth: 2
  :caption: Module 6 - Launchers
  :name: _m6
  :hidden:


.. toctree::
  :maxdepth: 2
  :caption: Module 7 - Remote Password Changers
  :name: _m7
  :hidden:


.. toctree::
  :maxdepth: 2
  :caption: Module 8 - Discovery
  :name: _m8
  :hidden:


.. toctree::
  :maxdepth: 2
  :caption: Module 9 - Auditing and Security
  :name: _m9
  :hidden:


.. _getting_started:

----------------
Before You Begin
----------------

Purpose
-------

This training and lab guide is designed to accompany a Thycotic trainer lead course. During your training course the trainer will regularly reference this guide as well as demonstrating lab exercises within a shared desktop environment and discussing common use cases and real-world scenarios.

Your training pack
------------------

Before you start this training course, ensure you have received lab details from your Thycotic trainer.
The Secret Server lab consists of the following machines:

.. list-table::
   :widths: 15 15 15 55
   :header-rows: 1

   * - Machine Name
     - Internal Lab Name
     - Internal IP
     - Description
   * - DC1
     - DC1
     - 172.31.32.10123
     - Domain Controller - contains all AD configuration used within the lab
   * - SS
     - SecretServer1
     - 172.31.40.114
     - This machine will be used to install and host Secret Server
   * - WIN
     - Client01
     - 172.31.46.76
     - Windows server, used to test a range of Secret Server functionalities during the training course
   * - CENTOS
     - 
     - 172.31.38.35
     - CentOS machine, used to test a range fo Secret Server functionalities during the training course


You will need to initiate a remote desktop connection to the **PUBLIC IP** address of the Win machine. This IP address is dynamic and will change whenever the lab environment is restarted. The Win server machine serves as a jump box from which you can then RDP to the other windows machines by hostname. Lab Exercise 1 explains the process of identifying the IP address of your lab jump box and connecting to it.

To log into the Virtual Machines with administrative rights, the below information is providing you the credentials for Windows and Linux.

**Windows Domain Admin Account**

| Username: **thylab\\adm-training**
| Password: **Thycotic@2019!**

**Centos SSH Account**

| Username: **thycotic**
| Password: **thycotest12$$**


