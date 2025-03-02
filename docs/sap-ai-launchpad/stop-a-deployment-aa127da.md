<!-- loioaa127da70b224c1c854fc4b1d3144647 -->

# Stop a Deployment

Stopping a deployment releases the computing resources acquired in the runtime in which the deployment is present \(such as SAP AI Core\).



<a name="loioaa127da70b224c1c854fc4b1d3144647__prereq_b54_nld_jpb"/>

## Prerequisites

You have the `mloperations_editor` or `scenario_deployment_editor` role, or you are assigned a role collection that contains this role. For more information, see [Roles and Authorizations](roles-and-authorizations-4ef8499.md).



<a name="loioaa127da70b224c1c854fc4b1d3144647__context_zoe_rnd_jpb"/>

## Context

You can stop a deployment if it has a *Running* or *Pending* status. For deployments in other statuses, the *Stop* button is not enabled.



<a name="loioaa127da70b224c1c854fc4b1d3144647__steps_z33_xqd_jpb"/>

## Procedure

1.  Navigate to the deployment's details. See [View a Deployment](view-a-deployment-d6f793e.md).

2.  Choose *Stop* in the header. A *Warning* dialog box appears.

3.  Choose *Stop* to stop running the deployment.




<a name="loioaa127da70b224c1c854fc4b1d3144647__result_rr1_4nd_jpb"/>

## Results

The deployment is stopped, and the computing resources that your deployment was using in the runtime instance are released.

**Related Information**  


[Stop Deployments](https://help.sap.com/viewer/2d6c5984063c40a59eda62f4a9135bee/CLOUD/en-US/b7d2577088c84417bbab370173d38cd8.html#loiob7d2577088c84417bbab370173d38cd8 "Stopping a deployment releases the SAP AI Core runtime computing resources that it used.") :arrow_upper_right:

