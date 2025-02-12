# Data-centric microservices walkthrough with Helidon MP

## Introduction

This lab will show you how to deploy the microservices on your Kubernetes cluster, walk through the functionality and explain how it works.

Estimated Lab Time - 10 minutes

Quick walk through on how to deploy the microservices on your Kubernetes cluster.

[](youtube:8gMmjbXSR68)

### Objectives

-   Deploy and access the microservices
-   Learn how they work

### Prerequisites

* An Oracle Cloud paid account or free trial. To sign up for a trial account with $300 in credits for 30 days, click [Sign Up](http://oracle.com/cloud/free).
* The OKE cluster and the Autonomous Transaction Processing databases that you created in Lab 1

## Task 1: Deploy all the Microservices and the FrontEnd UI

1.  Run the deploy script. This will create the deployment and pod for all the java images in the OKE cluster `msdataworkshop` namespace:

    ```
    <copy>cd $GRABDISH_HOME;./deploy.sh</copy>
    ```

   ![](images/deploy-all.png " ")

2.  Once successfully created, check that the services are running:

    ```
    <copy>kubectl get pods --all-namespaces</copy>
    ```

  ![](images/pods-all-after-deploy.png " ")

  Or, you can execute the `pods` shortcut command:

3. Check that the **ingress-nginx-controller** load balancer service is running, and write down the external IP address.

    ```
    <copy>kubectl get services --all-namespaces</copy>
    ```

    ![](images/ingress-nginx-loadbalancer-externalip.png " ")


  Or, you can execute the `services` shortcut command.

## Task 2: Access the FrontEnd UI

You are ready to access the frontend page. Open a new browser tab and enter the external IP URL:

`https://<EXTERNAL-IP>`

Note that for convenience a self-signed certificate is used to secure this https address and so it is likely you will be prompted by the browser to allow access.

You will be prompted to authenticate to access the Front End microservices. The user is `grabdish` and the password is the one you entered in Lab 1.

![](images/frontendauthlogin.png " ")

You should then see the Front End home page. You've now accessed your first microservice of the lab!

![](images/ui-home-page.png " ")

We created a self-signed certificate to protect the frontend-helidon service. This certificate will not be recognized by your browser and so a warning is displayed. It will be necessary to instruct the browser to trust this site to display the frontend. In a production implementation a certificate that is officially signed by a certificate authority should be used.

## Task 3: Verify the Order and Inventory Functionality of GrabDish store

1. Click **Transactional** under **Labs**.

   ![](images/tx-select.png " ")

3. Check the inventory of a given item such as sushi, by typing `sushi`
    in the `food` field and clicking **Get Inventory**. You should see the inventory
    count result 0.

   ![](images/tx-get-inventory.png " ")

4. (Optional) If for any reason you see a different count, click **Remove Inventory** to bring back the count to 0.

5. Let’s try to place an order for sushi by clicking **Place Order**.

   ![](images/tx-place-order-66.png " ")

6. To check the status of the order, click **Show Order**. You should see a failed
    order status.

   ![](images/tx-show-order-66.png " ")

   This is expected, because the inventory count for sushi was 0.

7. Click **Add Inventory** to add the sushi in the inventory. You
    should see the outcome being an incremental increase by 1.

   ![](images/tx-add-inventory.png " ")

8. Go ahead and place another order by increasing the order ID by 1 (67) and then clicking **Place Order**. Next click **Show Order** to check the order status.

   ![](images/tx-place-order-67.png " ")

   ![](images/tx-show-order-67.png " ")

   The order should have been successfully placed, which is shown by the order status showing success.

## Acknowledgements
* **Author** - Paul Parkinson, Developer Evangelist; Richard Exley, Consulting Member of Technical Staff, Oracle MAA and Exadata
* **Adapted for Cloud by** - Nenad Jovicic, Enterprise Strategist, North America Technology Enterprise Architect Solution Engineering Team
* **Documentation** - Lisa Jamen, User Assistance Developer - Helidon
* **Contributors** - Jaden McElvey, Technical Lead - Oracle LiveLabs Intern
* **Last Updated By/Date** - Richard Exley, April 2021
