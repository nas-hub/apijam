[Select_Shared_Flows]: ./media/Select_Shared_Flows.gif "Select the shared flow"
[Shared_Flows_Enterprise_Baseline_Security]: ./media/Shared_Flows_Enterprise_Baseline_Security.gif "Create Enterprise_Baseline_Security Sharfed Flow"
[Navigate_EditFlowHooks]: ./media/Navigate_EditFlowHooks.gif "Edit Flow Hooks"
[Trace_AutoEnforced_ESSB]: ./media/Trace_AutoEnforced_ESSB.gif "Test Flow Hooks"
[Navigate_SaveESBS_SharedFlow]: ./media/Navigate_SaveESBS_SharedFlow.gif "Save Flow Hooks"
[Navigate_Environments]: ./media/Navigate_Environments.gif "Navigate to Environments"
[SharedFlow_New_Pipeline]: ./media/SharedFlow_New_Pipeline.gif "New shared flow"
[SharedPolicy_ESBS_Save]: ./media/SharedPolicy_ESBS_Save.gif "Save Shared Flow"
[SharedPolicy_ESBS_Deploy]: ./media/SharedPolicy_ESBS_Deploy.gif "Deploy Shared Flow"
[Create_KVM_Shared_Flows]: ./media/Create_KVM_Shared_Flows.gif "Create new shared flow"
[RestClient_Create_KVM_Body]: ./media/RestClient_Create_KVM_Body.gif "Rest Client - Headers"
[RestClient_Create_KVM_Headers]: ./media/RestClient_Create_KVM_Headers.gif "Rest Client - Body"
[Policy_Retrieve_OIDC_Info]: https://github.com/adam-p/markdown-here/raw/master/src/common/images/icon48.png "Logo Title Text 2"


[Policy_Icon_Populate_Cache]: http://d3grn7b5c5cnw5.cloudfront.net/sites/docs/files/icon_policy_traffic-management.jpg "Logo Title Text 2"
[Policy_Icon_VerifyAPIKey]: http://d3grn7b5c5cnw5.cloudfront.net/sites/docs/files/icon_policy_security.jpg "Logo Title Text 2"
[Policy_Icon_ACL]: http://d3grn7b5c5cnw5.cloudfront.net/sites/docs/files/icon_policy_security.jpg "IP Blacklist Filter"
[Policy_Icon_RegEx]: http://d3grn7b5c5cnw5.cloudfront.net/sites/docs/files/icon_policy_threat-protection.jpg "Regular Expression Protection Policy"
[Policy_Icon_XMLTCP]: http://d3grn7b5c5cnw5.cloudfront.net/sites/docs/files/icon_policy_threat-protection.jpg "XML threat Protection Policy"
[Policy_Icon_JSONTCP]: http://d3grn7b5c5cnw5.cloudfront.net/sites/docs/files/icon_policy_threat-protection.jpg "JSON threat Protection Policy"
[Policy_Icon_BasicAuthentication]: http://d3grn7b5c5cnw5.cloudfront.net/sites/docs/files/icon_policy_threat-protection.jpg "Logo Title Text 2"
[Policy_Icon_FlowCallout]: http://d3grn7b5c5cnw5.cloudfront.net/sites/docs/files/icon_policy_flow-callout.png "Logo Title Text 2"
[Policy_Icon_LookupCache]: http://d3grn7b5c5cnw5.cloudfront.net/sites/docs/files/icon_policy_traffic-management.jpg "Logo Title Text 2"
[Policy_Icon_ServiceCallout]: http://d3grn7b5c5cnw5.cloudfront.net/sites/docs/files/icon_policy_service-callout.jpg "Logo Title Text 2"
[Policy_Icon_KVM]: http://d3grn7b5c5cnw5.cloudfront.net/sites/docs/files/icon_policy_key-value-map-operations.jpg "Key Value Map Operations"
[Policy_Icon_ExtractVariables]: http://d3grn7b5c5cnw5.cloudfront.net/sites/docs/files/icon_policy_extract-variable.jpg "Logo Title Text 2"



[Okta_OktaGeneralPage]: ./media/OktaGeneralPage.gif "Okta General Tab"
[Okta_OktaSSOPage]: ./media/OktaSSOPage.gif "Okta Sign-On Tab"



# Flow Hooks : Applying Enterprise Security Policies accross all API-Proxies.


*Duration : 45 mins*

*Persona : API Team*
_____
# Use Case

Enterprise security team has defined a security policy for all the APIs published in an enterprise. This API policy acts as the enterprise standard security policy, that will be governed by enterprise security team (Enhancements, updates etc).

_____
# Concerns
How can enterprise security team ensure that all API developers correctly develop and deploy this enterprise security policy.
How can enterprise security team govern any updates to this security policy without involving/impacting individual API developers from various business units and line of business.

_____
# How can Apigee Edge help?
Apigee [__**Flow Hook**__](http://docs.apigee.com/api-services/content/flow-hooks) fulfills this requirement by addressing above concerns. The Enterprise security team based on thier requirements come up with their enterprise standard security policy. This enterprise security policy materializes in Apigee as a __Shared Flow__. This __Shared Flow__ will be marked as a Flow Hook. Flow Hook once configured acts as global enforcers of this __Shared Flow__.

_____
# Enterprise Standard Baseline Security Policy
For this lab, we will develop a Shared Flow that represents following enterprise standard baseline security policy:
```
    All ingress API traffic MUST have Threatening Content protection, providing controls for SQL Injections, XSS.
    All ingress API traffic MUST have XML and JSON Complexity attack protection.
    All ingress API traffic MUST have IP black list filters.
```
_____

# Pre-requisites
1. You have an API from previous labs you can use to check if the enterprise security policies are being applied.
2. Note that all existing API proxies in this environment will be now protected by this enterprise security policy.



_____
# Instructions


1. Create a shared flow to Develop the above defined enterprise standard baseline security policy.
   * In Edge UI, navigate to **Develop -> Shared Flows** 
    ![Select Shared Flows][Select_Shared_Flows] 
   * Create new Shared Flow policy by clicking the + Shared Flow Button as shown in the figure above.
   * Enter the Shared Flow name as:[Your Initials Here]_Enterprise_Baseline_Security 
   * Enter the Shared Flow description as : "Standard Auto Enforced Baseline Security Flow" 
    ![Select Shared Flows][Shared_Flows_Enterprise_Baseline_Security] 


   * Click the Develop Tab to create the policies for Shared Flow ![Shared Flow pipeline][SharedFlow_New_Pipeline]

   #### Add Threatening Content Protection Policy [![Threatening Content Protection][Policy_Icon_RegEx]](http://docs.apigee.com/api-services/reference/regular-expression-protection)
   This policy protects all ingress API traffic from SQL Injections, XML and JSON Attacks as defines by Enterprise Security Baseline Policy.
   <table>
    <tr><td>Order</td><td>Policy Type</td><td>Flow Type</td><td>Policy Name</td><td>Policy Description</td></tr>
    <tr><td>1</td><td>__Regular Expression Protection policy__</td><td>Shared Flow</td><td>Threatening Content Protection</td><td>Enterprise Baseline policy for - Threatening Content Protection</td></tr>
   </table>

   **Policy Configuration**
    ```
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>

    ```
   
   #### Add XML Threat Protection policy [![XML Threat Protection policy][Policy_Icon_XMLTCP]](http://docs.apigee.com/api-services/reference/xml-threat-protection-policy)
   This Policy protects all ingress API traffic from XML Complexity Attacks by enforcing the structural restrictions on XML payloads following the Enterprise Standard Baseline Policy.
    <table>
        <tr><td>Order</td><td>Policy Type</td><td>Flow Type</td><td>Policy Name</td><td>Policy Description</td></tr>
        <tr><td>2</td><td>__XML Threat Protection policy__</td><td>Shared Flow</td><td>XML Complexity Attack Protection</td><td>Enterprise Baseline policy for - XML Complexity Attack Protection</td></tr>
    </table>
   **Policy Configuration**
    ```
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>

    ```
   
   #### Add JSON Threat Protection policy [![JSON Threat Protection policy][Policy_Icon_XMLTCP]](http://docs.apigee.com/api-services/reference/json-threat-protection-policy)
   This Policy protects all ingress API traffic from JSON Complexity Attacks by enforcing the structural restrictions on JSON payloads following the Enterprise Standard Baseline Policy.
   <table>
        <tr><td>Order</td><td>Policy Type</td><td>Flow Type</td><td>Policy Name</td><td>Policy Description</td></tr>
        <tr><td>3</td><td>__JSON Threat Protection policy__</td><td>Shared Flow</td><td>JSON Complexity Attack Protection</td><td>Enterprise Baseline policy for - JSON Complexity Attack Protection</td></tr>
    </table>
   **Policy Configuration**
    ```
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>

    ```
   
   #### Add Access Control policy [![JSON Threat Protection policy][Policy_Icon_ACL]](http://docs.apigee.com/api-services/reference/access-control-policy)
   This Policy blocks any call originating from black listed IP addresses by an Enterprise Strandard Baseline Security Policy.
    <table>
        <tr><td>Order</td><td>Policy Type</td><td>Flow Type</td><td>Policy Name</td><td>Policy Description</td></tr>
        <tr><td>4</td><td>__Access Control policy__</td><td>Shared Flow</td><td>IP Black List Filter</td><td>Enterprise Baseline policy for - Black list IP address filters</td></tr>
    </table>
   **Policy Configuration**
    ```
    <?xml version="1.0" encoding="UTF-8" standalone="yes"?>

    ```
   

2. Save the shared flow.
    ![Shared Flow pipeline][SharedPolicy_ESBS_Save] 

3. Deploy the shared flow.
    ![Shared Flow pipeline][SharedPolicy_ESBS_Deploy]   
    Now this shared flow is active and is available in the __test__ environment.

4. Assign Shared Flow to a Flow-Hook
    
    ![Shared Flow pipeline][Navigate_Environments] 

5. Edit Flow Hooks: Navigate to Environments and Select the Flow Hooks tab.
   ![Shared Flow pipeline][Navigate_EditFlowHooks] 

6. Save Flow Hooks
   ![Shared Flow pipeline][Navigate_SaveESBS_SharedFlow] 
    Once you Edit and connect the Pre-Proxy Flow Hook with the Shared Flow: The Shared Flow is in active and will be applied to all API Proxies accross __test__ environment.
7. Now the enterprise standard baseline security policy is active; For you to test this, select any proxies you created as part of Core labs and navigate to the trace tab of that API-Proxy. Start the Trace session and invoke the API from within the Trace tab. Ensure that this API-Proxy is deployed in __Test__ environment. As shown in the figure below you should be see the enterprise standard baseline security policy applied automatically for this API-Proxy.
   ![Shared Flow pipeline][Trace_AutoEnforced_ESSB] 



**Congratulations!**  You’ve done a cool thing here -- you developed a Enterprise Standard Baseline Security Policy and enabled it for an entire environment for an organization/enterprise. You also tested that the developed Flow Hook executes automatically for all API Proxies in that environment for your organization. Nice work!

# Lab Video

If you prefer to learn by watching, here is a video lab on using Flow Hooks

[https://youtu.be/55-tYJSVnNE](https://youtu.be/55-tYJSVnNE)

# Earn Extra-points

If your enterprise security baseline policy had an egress rules, where and how would you have implemented that as part of the Flow Hook.


# Quiz

1. Can you have a different Enterprise Security Policy per environment?
2. Is it only security related policies that can be enforced by Flow Hooks?
3. What if a API developer login into edge UI and disconnects the Flow Hook from Shared Flow?



# Summary

In this lab, you learned how to use Flow Hooks to automatically enforce a __**Shared Flow**__ for all API Proxies in selected environment.



# Rate this lab

How did you link this lab? Rate [here](https://docs.google.com/).
