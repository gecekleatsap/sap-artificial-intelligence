<!-- copy3a06d84313a5406f813d7cd7a0356d5d -->

# Choose a Resource Plan

You can configure SAP AI Core to use different infrastructure resources for different tasks, based on task demand. SAP AI Core provides several preconfigured infrastructure bundles called “resource plans” for this purpose.



<a name="copy3a06d84313a5406f813d7cd7a0356d5d__context_q1p_fpm_zqb"/>

## Context

Resource plans are used to select resources in workflow and serving templates. Different steps of a workflow can have different resource plans.

In general, if your workload needs or profits from GPU acceleration, you should use one of the GPU-enabled resource plans. Otherwise, choose the resource plan based on the anticipated CPU and memory need of your workloads.

Within SAP AI Core, the resource plan is selected via the `ai.sap.com/resourcePlan` label at pod level. It maps the resource plan selected by a user and uses the string value, which can be any of the following resource plan IDs:

**Resource Plan Specifications for AWS**


<table>
<tr>
<th valign="top">

Resource Plan IDs



</th>
<th valign="top">

GPUs



</th>
<th valign="top">

CPU Cores



</th>
<th valign="top">

Memory GBs



</th>
<th valign="top">

Code to Allocate Resources

\(to Add to Workflow Templates\)



</th>
</tr>
<tr>
<td valign="top">

Train-L



</td>
<td valign="top">

1 V100



</td>
<td valign="top">

7



</td>
<td valign="top">

55



</td>
<td valign="top">

`ai.sap.com/resourcePlan: train.l`



</td>
</tr>
<tr>
<td valign="top">

Infer-S



</td>
<td valign="top">

1 T4



</td>
<td valign="top">

3



</td>
<td valign="top">

10



</td>
<td valign="top">

`ai.sap.com/resourcePlan: infer.s`



</td>
</tr>
<tr>
<td valign="top">

Infer-M



</td>
<td valign="top">

1 T4



</td>
<td valign="top">

7



</td>
<td valign="top">

26



</td>
<td valign="top">

`ai.sap.com/resourcePlan: infer.m`



</td>
</tr>
<tr>
<td valign="top">

Infer-L



</td>
<td valign="top">

1 T4



</td>
<td valign="top">

15



</td>
<td valign="top">

58



</td>
<td valign="top">

`ai.sap.com/resourcePlan: infer.l`



</td>
</tr>
<tr>
<td valign="top">

Starter



</td>
<td valign="top">

–



</td>
<td valign="top">

1



</td>
<td valign="top">

3



</td>
<td valign="top">

`ai.sap.com/resourcePlan: starter`



</td>
</tr>
<tr>
<td valign="top">

Basic



</td>
<td valign="top">

–



</td>
<td valign="top">

3



</td>
<td valign="top">

11



</td>
<td valign="top">

`ai.sap.com/resourcePlan: basic`



</td>
</tr>
<tr>
<td valign="top">

Basic-8x



</td>
<td valign="top">

–



</td>
<td valign="top">

31



</td>
<td valign="top">

116



</td>
<td valign="top">

`ai.sap.com/resourcePlan: basic.8x`



</td>
</tr>
</table>

> ### Note:  
> There are limits to the default disk storage size for all of these nodes. Datasets that are loaded to the nodes will consume disk space. If you have large data sets \(larger than 30 GB\), or have large models, you may have to increase the disk size. To do so, use the persistent volume claim in Argo Workflows to specify the required disk size \(see [Volumes](https://argoproj.github.io/argo-workflows/walk-through/volumes/)\).

 <a name="loiocf3a9a5bb3f1476caf3099281da96a67"/>

<!-- loiocf3a9a5bb3f1476caf3099281da96a67 -->

## Service Usage Reporting

Usage consumption of services is reported in the SAP BTP cockpit on the *Overview* page for your global account and on the *Overview* and *Usage Analytics* pages of your subaccount. The usage report lists usage in billable measures and nonbillable measures. Your final monthly bill is based on the billable measure only. The nonbillable measures display usage for reporting purposes only.

