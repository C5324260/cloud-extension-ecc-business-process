# Setup of a SAP Business Technology Platform Account using Boosters
## Introduction

For running the ECC extension mission you will need the following services in your SAP Business Technology Platform (BTP) account.

* SAP Business Application Studio
* Event Mesh
* Cloud Foundry Runtime
* SAP HANA service for SAP BTP
* SAP Continuous Integration & Delivery Service (optional)

The entitlement differs for the pricing option of your account:

**Consumption-based SAP BTP Account:** 
No entitlement necessary. Be sure that you have enough credits to run the services.

**Subscription-based SAP BTP Account:** 
You have to create entitlements for the services above - [see also Entitlements and Quotas](https://help.sap.com/viewer/df50977d8bfa4c9a8a063ddb37113c43/Cloud/en-US/38ecf59cdda64150a102cfaa62d5faab.html#loio363f0f68f9704830ac65c87a2562559b).


[Check the costs with the SAP BTP Estimator Tool](https://www.sap.com/products/cloud-platform/pricing/estimator-tool.html?blueprintId=a0ad3bc5-4fcb-4008-b109-bd8f70634d6c)


**Booster:**

The setup could be done for each service individually. To simplify the setup process, SAP has introduced Boosters. Boosters are a collection of wizards that provides functionalities for specific scenarios to automate and speed-up the installation and configuration process of a SAP BTP sub-account. This also includes the user management with the mapping of the respective administrator and developer roles.

Before running the booster please check for which regions and infrastructures the services are available - [see SAP BTP Regions and Service Portfolio ](https://help.sap.com/doc/aa1ccd10da6c4337aa737df2ead1855b/Cloud/en-US/3b642f68227b4b1398d2ce1a5351389a.html) - unfortunately the booster is not able to check this in advance, so it will fail when you select a region where a service is not available.


**Persona:** Cloud Administrator (SAP BTP)

**Abbreviation:** SAP Business Technology Platform = SAP BTP

## Step-by-step

> The Booster **Prepare an account for Developing Extension Applications** is not available for trial accounts, if you're using a SAP BTP trial account please go to [section C for the manual setup](#manualSetup).  


### A: Run the Booster

1. Start the Booster
   Login to your global SAP BTP account.
   1. Select Boosters in the SAP BTP Account menu.
   2. Select **Extension Suite - Development Efficiency** from the drop-down list
   3. Select the Booster "Prepare an account for Developing Extension Applications"
   
   ![Booster](./images/booster-01.png)

2. Booster Overview

   ![Booster](./images/booster-02.png)
 
3. Select Components to get an overview of them. You can also view the cost estimate for running this scenario in a productive account. Choose **Start**

   ![Booster](./images/booster-03.png)

4. Check Prerequisites. If Ok press Next - otherwise check 
   ![Booster](./images/booster-04.png)


   > Hint: If you get a warning check which services are affected. If they are not relevant for this mission (see the next step) you can just ignore it.
   
   ![Booster Warning](./images/booster-04a.png)

5. Setup Subaccount
   
   - You find the list of the services that will acctivated by the Booster. For this mission the **Countinuous Integration & Delivery** service is optional. Remove it if you don't want to use it.
   - Services like **Alert Notification**, **Application Logging**, the **Extension Center**, the **Extension Factory serveless runtime**, **Launchpad** and the **SAP Cloud Transport Management Service** are not used in this  mission - therefore you can remove them. We will install the  **SAP HANA Cloud** DB in a separate step - so remove it also. 
   
   ![Booster](./images/booster-05.png)

   >By using a subscription-based SAP BTP account you have to set the quota of the **Cloud Foundry Runtime** to 3
   ![Booster](./images/booster-05a.png)
   
   1. In the sub section enter a meaningful Subaccount name - in general it reflects the organisation of your team etc.
   2. Select your Provider
   3. Select the Region
   4. Enter a meaningful Org Name
   5. Enter a space name - this should reflect the name of your project
   6. Press Next   
  
   ![Booster](./images/booster-06.png)

6. Add User
   1. Enter the User ID (mail address) of all administration users
   2. Enter the User ID (mail address) of all development users
   3. Press Next
   
   ![Booster](./images/booster-07.png)

7. Review your settings and press Finish
   
   ![Booster](./images/booster-08.png)

8.  Check the progess - all sections should get green
   
    ![Booster](./images/booster-09.png)

9. If you succeed navigate to the new Subaccount.

    ![Booster](./images/booster-10.png)

10. Check your subaccount: 
    Select Security - Role Collection
    You will find the Extension_App_Administrator and the Extension_App_Developer role collection. If you want to add additional users to the mission you have to assign one of those role collections.

    ![Booster](./images/booster-11.png)

    Go to **Instances and Subscriptions** and select the **Subscription** tab - check if the following subscriptions are enabled:
    * SAP Business Application Studio
    * Event Mesh
    * Continuous Integration & Delivery (only when selected in the booster)   
    
    ![Booster](./images/booster-12.png)

### B: Create a SAP HANA Service Instance

For this mission a SAP HANA service for SAP BTP is necessary. Use the following steps for activating it:

1. Select Services - Service Marketplace and choose the tile **SAP HANA Cloud**. If you do not see the **SAP HANA Cloud** tile, select **Entitlements** and choose **Configure Entitlements** and then choose **Add Service Plans** and assign the **SAP HANA Cloud** service with the **hana** service plan.

    ![HANA](./images/hana-01.png)

2. Select **Create**.
   
    ![HANA](./images/hana-02.png)

3. In the **New Instance** screen select 
    * Service = SAP HANA Cloud
    * Service Plan = Hana
    * Runtime Environment = Cloud Foundry
    * Space = the space you have created with the Booster
   
    click on the link **here** to create a Database first before creating an instance.
   

    ![HANA](./images/hana-03.png)

4. Choose the button **Create Database**.

    ![HANA](./images/createDatabase.png)


5.  Enter an 'Instance Name','Description' and 'Password'. if everything is correct then the **Step 2** button appear - choose it.

    ![HANA](./images/createDatabase02.png)

6.  Here you can setup the size of the SAP HANA Cloud instance - for the mission you can keep the minimum settings - select **Step 3**

    ![HANA](./images/hana-06.png)

7.  Keep the Advanced Settings and select **Create Instance**

    ![HANA](./images/hana07b.png)

8.  After some minutes the HANA instace is created and you should see a similar card.

    ![HANA](./images/hana-08.png)

With that the setup of your SAP BTP account is done.


### C: Manual Setup of Services and Authorization for BTP Trial Account
<a id="manualSetup"></a>
For running this mission on a SAP BTP trial account you have to enable the services and manage your authorizations by some manual steps: 


[Setup of SAP BTP Environment](https://help.sap.com/viewer/368c481cd6954bdfa5d0435479fd4eaf/Cloud/en-US/302b47b11e1749c3aa9478f4123fc216.html) gives you a general overview of a SAP BTP Cloud Foundry account.

For this mission we have to activate the following services:
  
* [Setup SAP Business Application Studio](https://help.sap.com/viewer/9d1db9835307451daa8c930fbd9ab264/Cloud/en-US/6331319fd9ea4f0ea5331e21df329539.html)
    * Subscribe to SAP Business Application Studio
    * Manage Authorization and Rules

* [Setup SAP Event Mesh](https://help.sap.com/viewer/bf82e6b26456494cbdd197057c09979f/Cloud/en-US/7e504322652d4791ade0ca2bbc5a6443.html)
    * See the setup for the deprecated Lite Service Plan  

* [Setup SAP Continous Integration and Delivery](https://help.sap.com/viewer/99c72101f7ee40d0b2deb4df72ba1ad3/Cloud/en-US/719acaf61e4b4bf0a496483155c52570.html)
  
    * Enabling the service
    * Assigning Roles and Permissions

* [Setup HANA Cloud Trial](https://www.sap.com/cmp/td/sap-hana-cloud-trial.html)
  
    * For the setup see **Section B**

