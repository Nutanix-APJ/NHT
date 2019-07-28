.. title:: Nutanix New Hire Training

.. toctree::
  :maxdepth: 2
  :caption: Installation and performance test
  :name: _labs
  :hidden:

  diyfoundation/diyfoundation
  xray/xray

.. toctree::
  :maxdepth: 2
  :caption: Files 
  :name: _labs
  :hidden:

  files_deploy/files_deploy

.. toctree::
  :maxdepth: 2
  :caption: Prism Central
  :name: _prism_central
  :hidden:
  
  prism_central_deploy/prism_central_deploy
  prism_central_features/prism_central_features

.. toctree::
  :maxdepth: 2
  :caption: Calm
  :name: _calm
  :hidden:

  calm_enable/calm_enable
  calm_projects/calm_projects
  calm_linux/calm_linux
  calm_win/calm_win
  calm_day2/calm_day2

.. toctree::
  :maxdepth: 2
  :caption: BCA
  :name: _labs
  :hidden:

  BCA/BCA

.. toctree::
  :maxdepth: 2
  :caption: Block Service
  :name: _labs
  :hidden:

  Volumes/volumes

.. toctree::
  :maxdepth: 2
  :caption: VDI
  :name: _labs
  :hidden:

   Frame/frame

.. toctree::
  :maxdepth: 2
  :caption: Appendix
  :name: _labs
  :hidden:

  tools_vms/windows_tools_vm
  tools_vms/linux_tools_vm


.. _getting_started:

Getting Started
===============

.. raw:: html

  <strong><font color="red">Do not start any labs before being told to do so by your
  instructor.</font></strong><br><br>

Welcome to Nutanix New Hire Training! Carefully review the **Overview** section of each lab before proceeding with the exercise.

In following steps, you may replace xx with your assigned cluster ID


Cluster Access
++++++++++++++

The Nutanix Hosted POC environment can only be accessed via VPN or virtual desktop. **It is recommended that the VPN be used to complete these labs.**

GlobalProtect VPN Access
........................

Browse to https://gp.nutanix.com.

Log in with your OKTA credentials.

Download and install the appropriate GlobalProtect agent for your operating system.

Launch GlobalProtect and configure **gp.nutanix.com** as the **Portal** address.

.. note::

  You can also leverage the legacy VPN solution, Pulse Secure. Connect and download the client from https://sslvpn.nutanix.com.

Virtual Desktop Access
.................

.. note::

If you are attending NHT and in a non-SE role (e.g. CSM, Services) you DO NOT have NUTANIXDC.local credentials. Alternate credentials are provided in class to access the HPOC Parallels VDI.
  
20 x VDI/VPN User Accounts: PHX-POC0XX-User01, PHX-POC0XX-User02 … PHX-POC0XX-User20 etc.
VDI/VPN User Password: techX2019!

xx is your cluster ID


Parallels VDI
1. Login to https://xld-uswest1.nutanix.com (for PHX) or https://xld-useast1.nutanix.com (for RTP) using your supplied credentials
2. Select HTML5 (web browser) OR Install the Parallels Client
3. Select a desktop or application of your choice.
  



