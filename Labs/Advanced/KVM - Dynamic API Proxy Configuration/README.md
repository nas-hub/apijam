# KVM : Dynamic API Proxy Configuration 

*Duration : 30 mins*

*Persona : API Team*

# Use case

You want your API Proxy to dynamically toggle configuration, there by some of the policies of any API Proxy are executed only when certain conditions are met. 

# How can Apigee Edge help?

By leveraging Apigee Key Value Map Policy (KVM), attributes based on which dynamic configuration is derived can be managed at Apigee. KVM provides management APIs to manage the stored values. KVM along with the Apigee Conditional tags can be leveraged to add Dynamic processing nature to API Proxies.
 
# Pre-requisites

Apigee Edge API Proxy created in core lab exercise. If not, jump back to "API Design - Create a Reverse Proxy with OpenAPI specification" lab.

# Instructions

1. Go to [https://apigee.com/edge](https://apigee.com/edge) and log in. This is the Edge management UI. 

2. Select **Admin → Environments** in the side navigation menu.

![image alt text](./media/Navigate_Environment.gif)

3. Select **test** as your environment and select the **Key Value Map** tab.

![image alt text](./media/Navigate_Key_Value_Map.gif)

4. Click New Key Value Map button to add a new Key Value Map.

![image alt text](./media/Click_New_KVM.gif)

5. Enter the Key Value Map name as __DynamicProxyConfig__.

![image alt text](./media/Dialog_New_KVM.gif)

6. Click New Key Value Map Entry button to add a new Key Value Map Entry.

![image alt text](./media/Add_New_KVM_Entry.gif)

7. Enter the Key name as __include_processing_stats_in_response__ and value as __ALL__. Click Save.

![image alt text](./media/Add_New_KVM_Entry_Values.gif)

8. You have configured a KVM and added an attribute entry that will be used in the API Proxy to dynamically configure the amount of processing stats sent back along with Response. 


## API Proxy Configuration

1. Select the {your-initials}_Employees_Proxy API proxy that you created in the Core Labs.

2. Click on **Develop** tab of {your-initials}_Employees_Proxy API proxy.

![image alt text](./media/Click_Develop_Tab.gif)

3. Click on **+Step** of the response of PreFlow as shown in the image below.

![image alt text](./media/Click_Response_Step.gif)

3. Select the __KeyValueMapOperations__ Policy from menu in left. Enter the name of the Policy as __LookUp_Dynamic_Proxy_Config__ and Click **Add** button.

![image alt text](./media/Add_KVM_Policy.gif)

3. Similarly Click on **+Step** one more time and add __AssignMessage__ Policy. Enter the name as "Add Processing Stats In Header" and Click **Add** button.

![image alt text](./media/Add_Assign_Message_Policy.gif)


4. Click on **Default** under Proxy Endpoint

![image alt text](./media/Click_Default_Flow.gif)


5. Add a Conditional Statement on the "Add Processing Stats In Header" Policy.

![image alt text](./media/Add_Conditional_Tag.gif)


5. Click on **Save** button.

![image alt text](./media/Save_Employee_Policy.gif)

5. Click on **Deploy** button, and deploy to test.

![image alt text](./media/Deploy_To_Test.gif)


## Test the API policy configuration

1. Open the  [Apigee Rest Client](https://apigee-rest-client.appspot.com/)  and run the Employee Proxy URL.

![image alt text](./media/Test_Screen_One.gif)

2. TODO...

*Congratulations!*...You have added 

# Earn Extra-points

TODO

# Quiz

1. TODO

2. TODO

# Summary

TODO

# References

* Useful Apigee documentation links on Traffic Management & Spike Arrest Policy  - 

     

# Rate this lab

How did you like this lab? Rate [here](https://goo.gl/forms/oivm4A6DqBKM9AEJ3).

