.. _karbon_deploy_vm:

---------------------------
Deploy KUBECTL from Calm 
---------------------------

Overview
++++++++

.. note::

  Estimated time to complete: **45 MINUTES**

  In this exercise you will create a Nutanix Calm Blueprint based on a Microsoft Windows 10 image.  The image will be sysprepped with an unattended XML answer file, and then will be added to a Domain via a Powershell script

.. note::

  

UPLOAD CALM BLUEPRINT
++++++++++++++++++++++
  
Download the Calm blueprint in https://matthewnutanixpublic.s3.us-east-2.amazonaws.com/Karbon101/Kubectl_client.json

Open the Chrome browser.  Click on Save As. Save the file as Kubectl.json to local disk.

Navigate to Calm blueprint, click **Upload Blueprint**

.. image:: images/karbon_deploy_vm_0.png

Select Kubectl_client.json and click on Open.

After the blueprint was uploaded into Prism Central, check the Kubectl_client blueprint

.. image:: images/karbon_deploy_vm_1.png

Scroll down and ensure the OS image: ubu-template.qcow2 was there.  If this image was not available, check back upload image session in previous lab.

.. image:: images/karbon_deploy_vm_2.png

Click on Credential.  Ensure the following credential are setup.  In the ubuntu credential, key in the nutanix/4u as password.

.. image:: images/karbon_deploy_vm_3.png


LAUNCH THE BLUEPRINT
+++++++++++++++++++

Click on **Launch**

Fill in the name.  Eg Kubectl_client.  Click on Create.

.. image:: images/karbon_deploy_vm_4.png

The Kubectl_client application was provisioning. Monitor the progress until provisioning of Kubectl_client was completed successfully.

.. image:: images/karbon_deploy_vm_5.png


VERIFICATION
+++++++++++++

Click on Services. Click on KubectlClient.  

.. image:: images/karbon_deploy_vm_6.png

Click on “Open Terminal”

You can now start creating the cluster, click **+ Create Kubernetes Clusters**

.. image:: images/karbon_deploy_cvm_7.png

Select the credential (Ubuntu Credential).  Click on Proceed

.. image:: images/karbon_deploy_cvm_8.png

Key in “which kubectl”

.. image:: images/karbon_deploy_cvm_9.png

The command here is to verify kubeclt is installed and to confirm the location so that it can be made executable.
