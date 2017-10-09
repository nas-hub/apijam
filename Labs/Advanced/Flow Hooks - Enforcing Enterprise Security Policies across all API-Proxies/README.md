[Select_Shared_Flows]: ./media/Select_Shared_Flows.gif "Select the shared flow"
[Shared_Flows_Enterprise_Baseline_Security]: ./media/Shared_Flows_Enterprise_Baseline_Security.gif "Create Enterprise_Baseline_Security Sharfed Flow"
[Navigate_EditFlowHooks]: ./media/Navigate_EditFlowHooks.gif "Edit __**Flow Hooks**__"
[Trace_AutoEnforced_ESSB]: ./media/Trace_AutoEnforced_ESSB.gif "Test __**Flow Hooks**__"
[Navigate_SaveESBS_SharedFlow]: ./media/Navigate_SaveESBS_SharedFlow.gif "Save __**Flow Hooks**__"
[Navigate_Environments_0]: ./media/Navigate_Environments.gif "Navigate to Environments"
[Navigate_Environments]: ./media/Navigate_Environments_1.gif "Navigate to Environments"
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


# Flow Hooks: Applying Enterprise Security Policies across all API-Proxies.


*Duration : 45 minutes*

*Persona : API Team*
_____
# Use Case

An Enterprise wants to enforce its API security policy on all APIs published across the enterprise. This security policy acts as the enterprise standard security policy, governed by enterprise security team.

_____
# Concerns
How can enterprise security team ensure that all API developers correctly develop and deploy this enterprise security policy.
How can enterprise security team govern any updates to this security policy without involving/impacting individual API developers from various business units and line of business.

_____
# How can Apigee Edge help?
Apigee [__**Flow Hook**__](http://docs.apigee.com/api-services/content/flow-hooks) fulfills this requirement by addressing above concerns. The Enterprise security team based on their requirements come up with their enterprise standard security policy. This enterprise security policy materializes in Apigee as a __Shared Flow__. This __Shared Flow__ will be marked as a Flow Hook. Flow Hook once configured acts as global enforcers of this __Shared Flow__.

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


## Create a new shared flow .
   1. In Edge UI, navigate to **Develop -> Shared Flows** 
    ![Select Shared Flows][Select_Shared_Flows] 
   2. Create new Shared Flow policy by clicking the + Shared Flow Button as shown in the figure above.
   3. Enter the Shared Flow name as:[Your Initials Here]_Enterprise_Baseline_Security 
   4. Enter the Shared Flow description as : "Standard Auto Enforced Baseline Security Flow" 
    ![Select Shared Flows][Shared_Flows_Enterprise_Baseline_Security] 
   5. Click the Develop Tab to create the policies for Shared Flow ![Shared Flow pipeline][SharedFlow_New_Pipeline]
<br>
<br>

## Develop the above defined enterprise standard baseline security policy
####  As you are in advanced labs you should by now, know how to add a new policy to your flow. You will create the below listed policies in the order they are listed, with provided name, description and policy configuration snippet.   
   1. Add Threatening Content Protection Policy [![Threatening Content Protection][Policy_Icon_RegEx]](http://docs.apigee.com/api-services/reference/regular-expression-protection)
   ##### This policy protects all ingress API traffic from SQL Injections as defines by Enterprise Security Baseline Policy.
   Add Threatening Content Protection Policy providing below Name and Description
<table>
<tr><td>Order</td><td>Policy Type</td><td>Policy Name</td><td>Policy Description</td></tr>
<tr><td>1</td><td>Regular Expression Protection policy</td><td>Threatening Content Protection</td><td>Enterprise Baseline policy for - Threatening Content Protection</td></tr>
</table>

   **Policy Configuration** (Copy this configuration and replace it with the default policy configuration)
```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<RegularExpressionProtection async="false" continueOnError="false" enabled="true" name="Threatening-Content-Protection">
    <DisplayName>Threatening Content Protection</DisplayName>
    <Properties/>
    <Source>request</Source>
    <IgnoreUnresolvedVariables>false</IgnoreUnresolvedVariables>
    <QueryParam name="query">
        <Pattern>[\s]*(?i)((delete)|(exec)|(drop\s*table)|(insert)|(shutdown)|(update)|(\bor\b))</Pattern>
    </QueryParam>
</RegularExpressionProtection>
        
```
   
   2. Add XML Threat Protection policy [![XML Threat Protection policy][Policy_Icon_XMLTCP]](http://docs.apigee.com/api-services/reference/xml-threat-protection-policy)
   ##### This Policy protects all ingress API traffic from XML Complexity Attacks by enforcing the structural restrictions on XML payloads following the Enterprise Standard Baseline Policy.
   Add XML Threat Protection Policy providing below Name and Description
<table>
    <tr><td>Order</td><td>Policy Type</td><td>Policy Name</td><td>Policy Description</td></tr>
    <tr><td>2</td><td>XML Threat Protection policy</td><td>XML Complexity Attack Protection</td><td>Enterprise Baseline policy for - XML Complexity Attack Protection</td></tr>
</table>
    
   **Policy Configuration**(Copy this configuration and replace it with the default policy configuration)
```
    
<XMLThreatProtection async="false" continueOnError="false" enabled="true" name="XML-Complexity-Attack-Protection">
       <DisplayName>XML Complexity Attack Protection</DisplayName>
       <NameLimits>
          <Element>50</Element>
          <Attribute>10</Attribute>
          <NamespacePrefix>10</NamespacePrefix>
          <ProcessingInstructionTarget>5</ProcessingInstructionTarget>
       </NameLimits>
       <Source>request</Source>
       <StructureLimits>
          <NodeDepth>5</NodeDepth>
          <AttributeCountPerElement>2</AttributeCountPerElement>
          <NamespaceCountPerElement>3</NamespaceCountPerElement>
          <ChildCount includeComment="true" includeElement="true" includeProcessingInstruction="true" includeText="true">3</ChildCount>
       </StructureLimits>
       <ValueLimits>
          <Text>150</Text>
          <Attribute>10</Attribute>
          <NamespaceURI>10</NamespaceURI>
          <Comment>10</Comment>
          <ProcessingInstructionData>10</ProcessingInstructionData>
       </ValueLimits> 
</XMLThreatProtection>

```
   
   3. Add JSON Threat Protection policy [![JSON Threat Protection policy][Policy_Icon_XMLTCP]](http://docs.apigee.com/api-services/reference/json-threat-protection-policy)
   ##### This Policy protects all ingress API traffic from JSON Complexity Attacks by enforcing the structural restrictions on JSON payloads following the Enterprise Standard Baseline Policy.
   Add JSON Threat Protection Policy providing below Name and Description
   <table>
        <tr><td>Order</td><td>Policy Type</td><td>Policy Name</td><td>Policy Description</td></tr>
        <tr><td>3</td><td>JSON Threat Protection policy</td><td>JSON Complexity Attack Protection</td><td>Enterprise Baseline policy for - JSON Complexity Attack Protection</td></tr>
    </table>
    
   **Policy Configuration**(Copy this configuration and replace it with the default policy configuration)
```
<JSONThreatProtection async="false" continueOnError="false" enabled="true" name="JSON-Complexity-Attack-Protection">
   <DisplayName>JSON Complexity Attack Protection</DisplayName>
   <ArrayElementCount>20</ArrayElementCount>
   <ContainerDepth>10</ContainerDepth>
   <ObjectEntryCount>15</ObjectEntryCount>
   <ObjectEntryNameLength>50</ObjectEntryNameLength>
   <Source>request</Source>
   <StringValueLength>500</StringValueLength>
</JSONThreatProtection>

```
   
   4. Add Access Control policy [![Access Control Policy][Policy_Icon_ACL]](http://docs.apigee.com/api-services/reference/access-control-policy)
   ##### This Policy blocks any call originating from black listed IP addresses by an Enterprise Standard Baseline Security Policy.
   Add Access Control Policy providing below Name and Description
   <table>
        <tr><td>Order</td><td>Policy Type</td><td>Policy Name</td><td>Policy Description</td></tr>
        <tr><td>4</td><td>Access Control policy</td><td>IP Black List Filter</td><td>Enterprise Baseline policy for - Black list IP address filters</td></tr>
   </table>
    
   **Policy Configuration**(Copy this configuration and replace it with the default policy configuration)
```
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<AccessControl async="false" continueOnError="false" enabled="true" name="IP-Black-List-Filter">
  <DisplayName>IP Black List Filter</DisplayName>
  <IPRules noRuleMatchAction = "ALLOW">
    <MatchRule action = "DENY">
      <SourceAddress mask="24">10.10.20.0</SourceAddress>
      <SourceAddress mask="24">10.10.30.0</SourceAddress>
      <SourceAddress mask="24">10.10.40.0</SourceAddress>
    </MatchRule>
  </IPRules>
</AccessControl>

```
   5. Save the shared flow.
    ![Shared Flow pipeline][SharedPolicy_ESBS_Save] 
    
   6. Deploy the shared flow.
    ![Shared Flow pipeline][SharedPolicy_ESBS_Deploy]   
   ##### Now this shared flow is active and is available in the __test__ environment.

</br>

##  Mark this Shared Flow as a Flow-Hook

   1. Assign Shared Flow to a Flow-Hook
      ![Shared Flow pipeline][Navigate_Environments] 
   2. Edit __**Flow Hooks**__: Navigate to Environments and Select the __**Flow Hooks**__ tab.
      ![Shared Flow pipeline][Navigate_EditFlowHooks] 
   3. Save __**Flow Hooks**__
      ![Shared Flow pipeline][Navigate_SaveESBS_SharedFlow] 
    Once you Edit and connect the Pre-Proxy Flow Hook with the Shared Flow: The Shared Flow is in active and will be applied to all API Proxies across __test__ environment.
   4. Now the enterprise standard baseline security policy is active; For you to test this, select any proxies you created as part of Core labs and navigate to the trace tab of that API-Proxy. Start the Trace session and invoke the API from within the Trace tab. Ensure that this API-Proxy is deployed in __Test__ environment. As shown in the figure below you should be see the enterprise standard baseline security policy applied automatically for this API-Proxy.
      ![Shared Flow pipeline][Trace_AutoEnforced_ESSB] 


<br>

**Congratulations!**  You’ve done a cool thing here -- you developed a Enterprise Standard Baseline Security Policy and enabled it for an entire environment for an organization/enterprise. You also tested that the developed Flow Hook executes automatically for all API Proxies in that environment for your organization. Nice work!

# Lab Video

If you prefer to learn by watching, here is a video lab on using __**Flow Hooks**__

[https://youtu.be/55-tYJSVnNE](https://youtu.be/55-tYJSVnNE)

# Earn Extra-points

If your enterprise security baseline policy had an egress rules, where and how would you have implemented that as part of the Flow Hook.


# Quiz

1. Can you have a different Enterprise Security Policy per environment?
2. Is it only security related policies that can be enforced by __**Flow Hooks**__?
3. What if a API developer login into edge UI and disconnects the Flow Hook from Shared Flow?



# Summary

In this lab, you learned how to use __**Flow Hooks**__ to automatically enforce a __**Shared Flow**__ for all API Proxies in selected environment.



# Rate this lab

How did you link this lab? Rate [here](https://docs.google.com/forms/d/e/1FAIpQLSfgFlU4hvPxhH7xh1R3UsqVYInoauyZGB_yf2MpKQ0R_FVQmw/viewform).
