<!-- loio20a8667ef19e4de59a4469cb542a7457 -->

# Serving Templates

You use serving templates to manage your serving instances at the level of the main tenant. Serving templates define how a model is to be deployed.

Serving templates are used to deploy one or more trained models on a model server, which process incoming inference requests and return the results from the machine learning model, and are stored in your git repository, where you can version them as required.

In SAP AI Core, serving templates are mapped as `executables`. Mapping requires certain attributes in the `metadata` section of your template.

Models are deployed using a simple Kubernetes Custom Resource Definition \(CRD\), which is provided by KServe. To deploy a model, you must provide a YAML specification that follows the KServe specification and that defines the required input parameters and artifacts.

To get started, copy the generic serving template below and add your own values as required. You can use any text editor with a YAML plugin to create the templates. Your YAML specification must follow the KServe specs and define the required input parameters and artifacts.



**Serving Template Parameter Details**


<table>
<tr>
<th valign="top">

Type



</th>
<th valign="top">

Parameter



</th>
<th valign="top">

Description



</th>
</tr>
<tr>
<td valign="top">

`name` \(mandatory\)



</td>
<td valign="top">

 



</td>
<td valign="top">

The executable ID. The executable ID must be unique among all executables available within the SAP AI Core main tenant.



</td>
</tr>
<tr>
<td valign="top">

metadata \(mandatory\)



</td>
<td valign="top">

`name`



</td>
<td valign="top">

Technical ID of the serving template that is used to uniquely identify the serving template. It is specified as the serving Template's executable ID, and therefore must be unique among all executables available within the SAP AI Core main tenant.



</td>
</tr>
<tr>
<td valign="top" rowspan="5">

annotations



</td>
<td valign="top">

`scenarios.ai.sap.com/description` \(optional\)



</td>
<td valign="top">

A description of the scenario to which this executable belongs.



</td>
</tr>
<tr>
<td valign="top">

`scenarios.ai.sap.com/name` \(mandatory\)



</td>
<td valign="top">

Scenario name, which is necessary for the AI API to discover a scenario.



</td>
</tr>
<tr>
<td valign="top">

`executables.ai.sap.com/description` \(optional\)



</td>
<td valign="top">

A description of the serving template.



</td>
</tr>
<tr>
<td valign="top">

`executables.ai.sap.com/name` \(mandatory\)



</td>
<td valign="top">

The name of the serving template.



</td>
</tr>
<tr>
<td valign="top">

`executables.ai.sap.com/cascade-update-deployments` \(optional\)



</td>
<td valign="top">

Setting to allow changes to the serving template to be cascaded to associated deployments. See [Change Serving Template and Update Deployments](change-serving-template-and-update-deployments-9555fe1.md).



</td>
</tr>
<tr>
<td valign="top" rowspan="2">

labels



</td>
<td valign="top">

`scenarios.ai.sap.com/id` \(mandatory\)



</td>
<td valign="top">

The scenario ID to which the serving template belongs



</td>
</tr>
<tr>
<td valign="top">

`ai.sap.com/version` \(mandatory\)



</td>
<td valign="top">

The version is intended for customer usage to identify compatible serving template versions.



</td>
</tr>
<tr>
<td valign="top" rowspan="3">

spec



</td>
<td valign="top">

`imagePullSecret`\(Optional\)

Not required if your Docker image is fetched from a public docker repository.



</td>
<td valign="top">

Name of your Docker registry secret. The name references your Docker credentials to fetch the image for your Docker container. For information about creating Docker registry secrets, see [Register Your Docker Registry Secret](register-your-docker-registry-secret-a7cf5e1.md).



</td>
</tr>
<tr>
<td valign="top">

`minReplicas` \(Optional\)



</td>
<td valign="top">

Deployments run continually by default, but can be stopped manually when inferences are not needed. Setting minReplicas to `0` allows the inference server to enter the stopped state, when not in use. When needed, it is restarted and nodes scaled, based on demand and the min/maxReplicas parameter.



</td>
</tr>
<tr>
<td valign="top">

`maxReplicas` \(Optional\)



</td>
<td valign="top">

Limit the number of nodes that the inference server scales up to.



</td>
</tr>
<tr>
<td valign="top">

labels \(mandatory\)



</td>
<td valign="top">

`ai.sap.com/resourcePlan`



</td>
<td valign="top">

You must specify the chosen `resourcePlan`. The value is the string value of the selected resource plan selected \(see [Choose a Resource Plan](choose-a-resource-plan-57f4f19.md)\).



</td>
</tr>
</table>



```
apiVersion: ai.sap.com/v1alpha1
kind: ServingTemplate
metadata:
  name: text-clf-infer-tutorial
  annotations:
    scenarios.ai.sap.com/description: "SAP developers tutorial scenario"
    scenarios.ai.sap.com/name: "text-clf-tutorial-scenario"
    executables.ai.sap.com/description: "Inference executable for text classification with Scikit-learn"
    executables.ai.sap.com/name: "text-clf-infer-tutorial-exec"
  labels:
    scenarios.ai.sap.com/id: "text-clf-tutorial"
    ai.sap.com/version: "1.0.0"
spec:
  inputs:
    parameters: []
    artifacts:
      - name: textmodel
  template:
    apiVersion: "serving.kserve.io/v1beta1"
    metadata:
      annotations: |
        autoscaling.knative.dev/metric: concurrency
        autoscaling.knative.dev/target: 1
        autoscaling.knative.dev/targetBurstCapacity: 0
      labels: |
        ai.sap.com/resourcePlan: starter
    spec: |
      predictor:
        imagePullSecrets:
        - name: <Name of your Docker registry secret>
        minReplicas: 0
        maxReplicas: 5
        containers:
        - name: kserve-container
          image: "<DOCKER IMAGE URL GOES HERE>"
          ports:
            - containerPort: 9001
              protocol: TCP
          env:
            - name: STORAGE_URI
              value: "{{inputs.artifacts.textmodel}}"
```



-   STORAGE\_URI environment variable name is currently hard-coded in KServe to indicate that the model should be downloaded when a custom predictor is configured with the env varSTORAGE\_URI.
-   /mnt/models is currently hard-coded in KServe. When you try this example with your own docker container, read the models from that path.



<a name="loio20a8667ef19e4de59a4469cb542a7457__section_m4l_4cy_3wX"/>

## Sync an Application Manually



### Applications sync with your GitHub repository automatically at intervals of ~3 minutes. Use the endpoint below to manually request a sync:

`{{apiurl}}/admin/applications/{{appName}}/refresh`

-   **[Serving Template API Reference](serving-template-api-reference-51b2271.md "")**  

-   **[Change Serving Template and Update Deployments](change-serving-template-and-update-deployments-9555fe1.md "If you change a serving template, you can automatically update the deployments that are associated with that template.")**  
If you change a serving template, you can automatically update the deployments that are associated with that template.

**Parent topic:** [Use Your Model](use-your-model-7f93e8f.md "You deploy your AI learning model to run inferences against it.")

**Related Information**  


[Choose a Resource Plan](choose-a-resource-plan-8deca74.md "You can configure SAP AI Core to use different infrastructure resources for different tasks, based on task demand. SAP AI Core provides several preconfigured infrastructure bundles called “resource plans” for this purpose.")

[List Executables](list-executables-6af8e60.md "An executable is a template that is instantiated for a purpose, such as training a model or creating a deployment. You can list all of the executables in a resource group and get details of specific executables from a resource group. Serving templates are mapped to deployment executables.")

[Deploy Models](deploy-models-dd16e8e.md "Utilize your model and retrieve a URL to use for inferencing.")

[Inference](inference-e348ecf.md "Use the URL from your model deployment to access the results of your model.")

[Update a Deployment](update-a-deployment-9789ddd.md "You can update a deployment with a new configuration while retaining the inference URL.")

[Stop Deployments](stop-deployments-b7d2577.md#loiob7d2577088c84417bbab370173d38cd8 "Stopping a deployment releases the SAP AI Core runtime computing resources that it used.")

[Delete Deployments](delete-deployments-0193d17.md#loio0193d17a7bdb4ae08a9c8301d1d8c1b8 "Deleting a deployment releases the SAP AI Core resources that it used.")

[Efficiency Features](efficiency-features-9fad26a.md "Discover features of SAP AI Core that improve model server efficiency and help manage resource consumption.")

[Retrieve Deployment Logs](retrieve-deployment-logs-4c86b88.md "Information about API processing and metrics, are stored and accessed in the deployment and execution logs.")

 <a name="concept_dcw_41k_lwb"/>

<!-- concept\_dcw\_41k\_lwb -->

## Stop or Delete Multiple Deployments



The feature is set to false by default. To enable bulk PATCH operations, your template must contain the following snippet, with the relevant values set to `true`.

```

Meta:
  "bulkUpdates": {
        "executions": false,
        "deployments": false
      }
```

**Related Information**  


[Stop Multiple Deployments](stop-deployments-b7d2577.md#loio331cdf505d1c47618256a83920dd7c9a "")

[Delete Multiple Deployments](delete-deployments-0193d17.md#loio6b521aa3dfa1465a9be658bdb38fb2e5 "")

