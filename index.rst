.. title:: Delinea - Privilige Manager Handson Training

.. toctree::
   :maxdepth: 2
   :caption: Module 1 - Installation
   :name: _m1
   :hidden:

   module1/module1

.. toctree::
  :maxdepth: 2
  :caption: Module 2 - Licensing 
  :name: _m2
  :hidden:

  module2/module2   

.. toctree::
  :maxdepth: 2
  :caption: Module 3 - Agent installation
  :name: _m3
  :hidden:

  module3/module3

.. toctree::
  :maxdepth: 2
  :caption: Module 4 - Active Directory
  :name: _m4
  :hidden:

  module4/module4

.. toctree::
  :maxdepth: 2
  :caption: Module 5 - Policy Overview
  :name: _m5
  :hidden:

  module5/module5

.. toctree::
  :maxdepth: 2
  :caption: Module 6 - Run as Admin Policy
  :name: _m6
  :hidden:

  module6/module6


.. toctree::
  :maxdepth: 2
  :caption: Module 7 - Global Policies
  :name: _m7
  :hidden:

  module7/module7

.. toctree::
  :maxdepth: 2
  :caption: Module 8 - Targeted Policies
  :name: _m8
  :hidden:

  module8/module8

.. toctree::
  :maxdepth: 2
  :caption: Module 9 - Local Security
  :name: _m9
  :hidden:

  module9/module9

.. _getting_started:

----------------
Before You Begin
----------------

Purpose
-------

This training and lab guide is designed to accompany a Delinea trainer lead course. During your training course the trainer will regularly reference this guide as well as demonstrating lab exercises within a shared desktop environment and discussing common use cases and real-world scenarios.

Your training pack
------------------

Before you start this training course, ensure you have received lab details from your Delinea trainer.
The Secret Server lab consists of the following machines:

.. list-table::
   :widths: 15 15 70
   :header-rows: 1

   * - Machine Name
     - Internal Lab Name
     - Description
   * - DC1
     - DC1
     - Domain Controller - contains all AD configuration used within the lab
   * - SSPM
     - SSPM
     - This machine will be used to install and host Privilege Manager
   * - Client
     - Client01
     - Windows server, used to test a range of Privilege Manager functionalities during the training course


| All lab machines can be accessed easily from the Skytap URL provided by your trainer.
|
| The administrative credentials you will need to log into the lab machines:
|
| **Windows Domain Admin Account**
| Username: thylab\\adm-training
| Password: *Password will be provided by trainer*
|
| **Windows Domain Standard User Account (for testing policy)**
| Username: thylab\\StandardUser
| Password: *Password will be provided by trainer*


Introduction
------------

Your trainer will provide a slide-based introduction to Privilege Manager, the slide deck used will
be shared.

General remark
--------------

When logging into the Client01 VM as "normal" none administrative account, please be patient as due to new updates of Windows that have been installed, lots needs to be updated in the backend... It may take 1-3 minutes per user. Also the first time you open the Privilege Manager UI it will take time to get IIS ready to serve the UI. This is only on the first time the UI is opened.

Versioning
**********

.. list-table::
   :widths: 15 15 15 55
   :header-rows: 1

   * - Date 
     - Author
     - Version
     - Description
   * - 1st Dec 2021
     - WE 
     - 1.2
     - Updated to reflect version 11.2.x
   * - 7th June 2022
     - WE 
     - 4.0
     - Updated to reflect version 11.3.x as well as new agent and Windows updates
  
 


