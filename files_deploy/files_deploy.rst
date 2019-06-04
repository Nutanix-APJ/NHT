.. _files_deploy:

---------------
 File Services
---------------

Overview
++++++++

.. note::

  Estimated time to complete: **1 HOUR**

In this exercise you will use Prism to deploy Files, a native, distributed file server solution for Nutanix clusters. You will configure SMB share, and familiarize yourself with new features of the AFS offering.

In following steps, you may replace xx with your assigned cluster ID



Networks preparation
+++++++++++++++++++++

Launch a web browser and log into POCxx-ABC PRISM with IP 10.42.xx.37, User: admin, Password: techX2019!

Firstly, we need to make sure a primary and a secondary network are created for File Service. 

Click gear icon on top right to access configuration page and navigate to Network Configuration. Click **+Create Network** in **Virtual Networks** tab.

- create ‘Rx-Automation-Network’ with VLAN 0
 
- create vlan *z* (*z* should be replaced by xx1; eg. if your cluster ID xx is 4, then *z* is 41) named **Secondary** 

then click **save**



.. image:: images/image001.png


  
Create AD VM for AD/LDAP connectivity
+++++++++++++++++++++++++++++++++++++++++
In Prism>Storage , create a Storage Container called **Images** if there is no existing one of that name.

Using an SSH client, connect to the Node A CVM IP <10.42.xx.29> in your assigned block using the following credentials:

Username - nutanix

Password - default

Execute the following commands to upload AD image:

.. code-block:: bash

  acli image.create AutoDC container=Images image_type=kDiskImage source_url=https://s3.amazonaws.com/get-ahv-images/AutoDC2.qcow2



Now we are going to create an AD VM from image AutoDC. AD is a pre-requirement of File Service.

In **Prism > VM**, click **+ Create VM**


.. image:: images/image003.png

.. image:: images/image004.png


   
click **+ Add New Disk** , choose **Clone from Image Service** and image ‘AutoDC’，click **Add**.


.. image:: images/image005.png


Click **+Add new NIC** and choose **Rx-Automation-Network** vlan.0, click **Add**.


.. image:: images/image006.png 

 
After AD VM is created successfully, power on AD VM, then launch console to see domain name, IP Address and credentials of AD. This information will be used later.


.. image:: images/image008.png


Deploy Acropolis File Services
++++++++++++++++++++++++++++++

In **Prism > File Server**, click **+ File Server**.


Firstly, download Files 3.2.0.2 package, click **Continue** to install File Services Software on POCxx.
Secondly, add Data Services IP as 10.42.xx.38. Click Continue.


.. image:: images/image009.png


Fill out the following fields and click **Next**:

- **Name** - *intials*-Files (e.g. POCxx-Files)
- **Domain** - ntnxlab.local
- **File Server Size** - 1 TiB
  
  
.. image:: images/image010.png


Select the **Rx-Automation-Network-Unmanaged** VLAN for the Client Network. Specify your cluster's **AutoDC** VM IP as the **DNS Resolver IP**. Click **Next**.

.. note::

  In order for the Files cluster to successfully find and join the **ntnxlab.local** domain it is critical that the **DNS Resolver IP** is set to the **AD** VM IP **FOR YOUR CLUSTER**. By default, this field is set to the primary **Name Server** IP configured for the Nutanix cluster, **this value is incorrect and will not work**.

Fill out the following fields and click **Next**:

- **Subnet Mask** – 255.255.255.128
- **Gateway** – 10.42.xx.1
- **IP** – **from** 10.42.xx.100 **to** 10.42.xx.102 (click **save** on the right)
- **DNS** – 10.42.xx.yz (check AD VM IP address)
- **NTP** – 0.pool.ntp.org


.. image:: images/image011.png



.. image:: images/image012.png



.. note::

 Files requires n (n, being the number of FSVMs) IP addresses on the Client network: 1 IP address per FSVM.

Select the **Secondary - Managed** VLAN for the Storage Network. Click **Next**.

Fill out the following fields and click **Next**:

- **Subnet Mask** – 255.255.255.128
- **Gateway** – 10.42.xx.129
- **IP** – **from** 10.42.xx.132 **to** 10.42.xx.135 (click **save** on the right)



.. image:: images/image013.png



.. note::
  
  AFS requires n+1 (n, being the number of FSVMs) IP addresses on the Storage network: 1 IP address per FSVM and 1 IP address for the CVMs to reach the FSVM cluster. This additional IP address is a floating highly available IP address. These IP addresses should not overlap with the IP addresses on the Client network.
  It is typically desirable to deploy Files with dedicated networks for client and storage. By design, however, Files does not allow client connections from the storage network in this configuration.

Fill out the following fields and click **Next**:

- Select **Use SMB Protocol**
- **Username** - Administrator@ntnxlab.local
- **Password** - See record from the console
- Select **Make this user a File Server admin**
- Select **Use NFS Protocol**
- **User Management and Authentication** - Unmanaged


.. image:: images/image015.png


Fill out the following fields and click **Create**:

- Select **Create a Protection Domain and a default schedule (highly recommended)**
- **PROTECTION DOMAIN NAME** - NTNX-POCxx-Files


.. image:: images/image016.png


Monitor deployment progress in **Prism > Tasks**.


.. image:: images/image017.png


.. note::

  If you receive a warning regarding DNS record validation failure, this can be safely ignored. The shared cluster does not use the same DNS servers as your Files cluster, and as a result is unable to resolve the DNS entries created when deploying Files.

Upon completion, select the **AFS** server and click **Protect**. Click **+Add schedule** to make a snapshot schedule you plan.


.. image:: images/image018.png


Observe the default Self Service Restore schedules, this feature controls the snapshot schedule for Windows' Previous Versions functionality. Supporting Previous Versions allows end users to roll back changes to files without engaging storage or backup administrators. Note these local snapshots do not protect the file server cluster from local failures and that replication of the entire file server cluster can be performed to remote Nutanix clusters. Click **Close**.

Configuring SMB Home Share
+++++++++++++++++++++++++++

In **Prism** > **File Server**, click **+Share/Export**. 

Fill out the following fields and click Next:
- **Name** – home
- **File Server**- POCxx-Files
- **Select Protocol** - SMB
 
 
.. image:: images/image019.png


Select **Enable Access Based Enumeration (ABE)**, **Self Service Restore** and **Advanced Settings**. Select **Home directory and User Profiles** and click **next**


.. image:: images/image020.png


Review Summary tab and click **create**
 
 
.. image:: images/image021.png


Parallels VDI 1. Login to https://xld-uswest1.nutanix.com (for PHX) or https://xld-useast1.nutanix.com (for RTP) using your supplied credentials belowed 2. Select HTML5 (web browser) OR Install the Parallels Client 3. Select a desktop or application of your choice.

20 x VDI/VPN User Accounts: PHX-POC0xx-User01, PHX-POC0xx-User02 … PHX-POC0xx-User20 etc. VDI/VPN User Password: techX2019!


.. image:: images/image022.png


You can see home share after login successfully.


.. image:: images/image023.png


You can also use domain name (\\POCxx-Files.ntnxlab.local) to access if you direct DNS of your desktop to AD VM IP(10.42.xx.yy).
