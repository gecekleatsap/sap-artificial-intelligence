<!-- loiod25b6b4e96fd4d39a71037ff1fa1852f -->

# Stop Multiple Deployments



<a name="loiod25b6b4e96fd4d39a71037ff1fa1852f__prereq_u4j_sld_nwb"/>

## Prerequisites

You have the `mloperations_editor` or `scenario_deployment_editor` role, or you are assigned a role collection that contains this role. For more information, see [Roles and Authorizations](roles-and-authorizations-4ef8499.md).



## Context

-   The maximum number of updates per request is 100.

-   Only *stopped*, *dead* or *unknown* executions or deployments can be deleted.

-   Only *running* or *pending* executions or deployments can be stopped.




<a name="loiod25b6b4e96fd4d39a71037ff1fa1852f__steps_lyt_xrj_nwb"/>

## Procedure

1.  Choose a resource group. For more information, see [Set Resource Group](set-resource-group-0c07728.md#loio0c077289f29d4147921fb07ab0f68b7f).

2.  In the *ML Operations* app, choose *Deployments*.

    The *Deployments* screen appears listing all of the deployments for the selected resource group. Deployments are listed by ID, and with additional details such as Name,Current and Target Status, Created On timestamp, and Changed On timestamp.

3.  Choose the Deployments you want to stop, using the checkboxes.

4.  Choose *Stop* in the header.




<a name="loiod25b6b4e96fd4d39a71037ff1fa1852f__result_lg1_yc4_4wb"/>

## Results

A dialog box appears, confirming how many of your selected deployments will be stopped.

> ### Note:  
> Where executions or deployments with a mixture of states that can be stopped **and** deleted are selected, only items eligible to the chosen request will be successfully processed.

