# Set Up a Fleet

## Introduction

This lab walks you through the steps to set up a new fleet in Java Management Service (JMS).

Estimated Time: 10 minutes

### Objectives

In this lab, you will:

* Set up a Fleet using the Java Management Service console interface

### Prerequisites

* You have signed up for an account with Oracle Cloud Infrastructure and have requested workshop reservation on LiveLabs.

## Task 1: Set Up Java Management Service Fleet

1. In the Oracle Cloud Console, open the navigation menu, click **Observability & Management**, and then click **Fleets** under **Java Management**.

     ![image of console navigation to java management service](images/console-navigation-jms.png)

2. Under the compartment section at the left, expand the compartment **LiveLabs**.

    Select the sub compartment **LLxxxxx-COMPARTMENT** indicated in your Login Info (Compartment should be under **jmslivelabs(root)** -> **LiveLabs**).

    ![image of compartment list in fleets](images/compartment-list-in-fleet.png)

    ![image of reservation info compartment](images/reservation-info-compartment.png)

    >**Note:** There is an occasional issue with the compartment naming which is in the midst of being resolved. If the compartment stated in the reservation info cannot be found in the **LiveLabs** compartment or if there is a **Authorization failed or requested resource not found error** in that compartment, refer to the troubleshooting guide [here](#TroubleshootFleetsetupissues).

    ![image of view compartment fleet error](images/view-compartment-fleet-error.png)

3. Click **Create Fleet**.

     >**Note:** You **do not** need to click **Inspect Prerequisites** here as the prerequisites are already set up for you.

     ![image of create new fleet](images/create-fleet-create-new.png)

4. In the **Fleet details** dialog box, enter a description in the **Fleet description** field.

   Keep the **default fleet name** here (for example, fleet-20230615-1135).

   Ensure that **Create operation log** is checked.

   ![image of create fleet options page](images/create-fleet-description.png)

5. Under advanced features, check the box for **Select all advanced features**.

   ![image of create fleet options page](images/create-fleet.png)

   Click **Agree**. This enables all the advanced features. You can still change the enabled advanced features after the fleet is created.

   ![image of agree advanced features](images/select-advanced-agree.png)

   There are 6 different advanced features available:
    - Lifecycle management (LCM) - Manage the lifecycle of Java runtimes in your fleet by installing or removing reported Java runtime.
    - Advanced usage tracking - Gain advanced insights into your Java workloads in the fleet by tracking application server, Oracle JDK and OpenJDK used by applications.
    - Crypto event analysis - Assess the impact of Oracle JRE and JDK Cryptographic roadmap on applications running in your fleet.
    - Performance analysis - Optimize Java workload performance with JVM tuning recommendations.
    - JDK Flight Recorder (JFR) - Collect information about events in the application running in your fleet using JDK Flight Recorder (JFR), a tool for collecting diagnostic and profiling data about a running Java application.
    - Java migration analysis - Evaluate the effort and feasibility of migrating Java applications to newer JDK versions.


   To learn more about the advanced features available, see [Using Java Management Service Advanced Features](https://apexapps.oracle.com/pls/apex/dbpm/r/livelabs/view-workshop?wid=3202).

6. Click **Next**.
    ![image of create fleet next](images/create-fleet-next.png)

7. You are prompted to review the fleet information, log configuration details and management agent configuration.

8. Click **Create**. This creates a new fleet and its configuration.
    ![image of create fleet confirm creation](images/create-fleet-create.png)

    >**Note:** If you wish to modify your choices, click **Previous**.

9. Wait for the progress to complete. 2 errors related to the **Dynamic group** and **Policies** creation for the **Advanced features** will pop up.

   Ignore these errors as these policies and dynamic groups has already been configured.

    > **Note:** For the sandbox environment, customized policies and dynamic groups have been pre-configured and sandbox users will not experience any disruptions. These error messages can be safely ignored, they arise from the policies and dynamic groups needing an administrator with necessary privileges at fleet creation, which sandbox users have not been granted.

    ![image of create fleet progress error](images/create-fleet-progress-error.png)

10. Scroll down and click **Download software and installation script**.

   ![image of page to download installation script](images/download-installation-script.png)

   Under the download installation script, select the Linux version of the installation script and click to download it.

   ![image of page to select installation script os](images/download-installation-script-os.png)

    Click **Close** once the download is complete. The downloaded file will be used in [Lab 2: Install Management Agent on your Managed Instances using Cloud Shell](?lab=install-management-agent-script) to install the Management Agent. You can still download the installation script after the fleet is created.

    Click **Cancel**. The **Done** button is not enabled due to the errors in the policies and dynamic group creation.

    ![image of page to create fleet cancel button](images/create-fleet-cancel.png)

11. On the **Java Management** page, click on the fleet that was created.
    ![image of fleet-created](images/fleet-created-compartment.png)

12. A **Log group inaccesible** error will be displayed at the top of the Fleet details page. This is related to the errors when creating the fleet. Click **Enable log configuration**. This will enable the logs required for the fleet.

    ![image of fleet-created](images/fleet-enable-logs.png)

13. Wait for the fleet to update.

    Another error, **Crypto log object is deleted** should appear. Click on the **Enable crypto log**. This will enable the logs for the crypto event analysis.
    ![image of fleet-created](images/fleet-enable-crypto-logs.png)

14. Wait for the fleet to update. All the advanced features should be enabled and the required logs should be active.
    ![image of fleet details page](images/fleet-details-page-main.png)

15. After JMS is linked to the management Agent, it will collect information on your Java runtimes. The rate at which the information is updated is dependent on the scan frequency of the management Agent on the instance. This may not occur immediately. The scanning frequency can be changed from the Fleet details page.

16. In the Fleet details page, click **More actions** and select **Modify agent settings**.
   ![image of fleet details page actions](images/fleet-details-page-new.png)

17. An **Agent settings** window will appear with the following settings:

    **Java runtime usage in minutes**: specify the frequency at which the management agent must report Java usage to JMS. The values must be between 5 and 90 minutes. The default value is 5 minutes.

    **Agent polling interval**: specify the frequency at which the management agent must check the work requests. For example, if the value specified is 10 minutes, the agent checks the work requests every 10 minutes and executes them. The values must be between 10 minutes and 12 hours. The default value is 10 minutes.

    **Work request validity**: specify the time for JMS to store the work requests. The values must be between 7 to 30 days. The default value is 2 weeks.

    **Java runtime discovery**: specify frequency at which the management agents should scan their hosts for Java runtime installations. The values must be between 3 to 24 hours. The default value is 24 hours.

18. For the purpose of this workshop, change **Java runtime usage in minutes** to **5 minutes**, and **Java runtime discovery** to **3 hours**.
    ![image of modify agent settings page](images/fleet-modify-agent-settings-new.png)

19. Click **Save changes** to save the new setting.
    ![image of save modify changes page](images/fleet-modify-agent-settings-save.png)

You may now **proceed to the next lab**.

## Troubleshoot Fleet set up issues

If you encounter **Authorization failed or requested resource not found error**, refer to the following steps.

* Locating the correct compartment:

     - Ensure that you are viewing a sub compartment in **LiveLabs**.

       ![image of compartment list in fleets](images/compartment-list-in-fleet.png)

     - Check for other compartments named **ZZ-EMPTY-20XXXXXX-XXXXXX-XXXX**.

       ![image of empty fleet name](images/empty-fleet-name.png)

     - Select the compartment. Check that able to show **No fleets found**.

       ![image of empty fleet error free](images/empty-fleet-error-free.png)
     
     - You may have to check all the **ZZ-EMPTY** compartments if there are multiple of them.

     - The compartment where you are able to view 'No fleets found' has the permissions for fleet creation, even though the compartment name is different from login page details. Utilise this compartment for subsequent steps.

## Learn More

* Refer to the [Using the Java Management Service Console](https://docs.oracle.com/en-us/iaas/jms/doc/using-java-management-service.html) section of the JMS documentation for more details.

* Refer to the [Enabling Advanced Features](https://docs.oracle.com/en-us/iaas/jms/doc/advanced-features.html#GUID-F5F4C42D-7BBB-4448-B898-82E4F7E999FB) section of the JMS documentation for details on how to enable advanced features.

* Use the [Troubleshooting](https://docs.oracle.com/en-us/iaas/jms/doc/troubleshooting.html#GUID-2D613C72-10F3-4905-A306-4F2673FB1CD3) chapter for explanations on how to diagnose and resolve common problems encountered when installing or using Java Management Service.

* If the problem still persists or it is not listed, then refer to the [Getting Help and Contacting Support](https://docs.oracle.com/en-us/iaas/Content/GSG/Tasks/contactingsupport.htm) section. You can also open a support service request using the **Help** menu in the OCI console.



## Acknowledgements

* **Author** - Yixin Wei, Java Management Service
* **Last Updated By** - Ivan Eng, June 2023
