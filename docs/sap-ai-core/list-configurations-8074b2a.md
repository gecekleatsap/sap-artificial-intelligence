<!-- loio8074b2a206cb41a2a68ba149a2150ea1 -->

# List Configurations

You can list all of the configurations in a resource group.



<a name="loio8074b2a206cb41a2a68ba149a2150ea1__section_a2q_fps_vnb"/>

## Using Postman

1.  Create a new GET request and enter the URL `{{apiurl}}/v2/lm/configurations`

2.  On the *Authorization* tab, set the type to *Bearer Token*.

3.  Set the token value to ***\{\{token\}\}***.

     ![](images/Bearer_Token_d6813f2.png) 

4.  On the *Header* tab, add the following entry:


    <table>
    <tr>
    <th valign="top">

    KEY


    
    </th>
    <th valign="top">

    VALUE


    
    </th>
    </tr>
    <tr>
    <td valign="top">

     `ai-resource-group` 


    
    </td>
    <td valign="top">

     *<Name of your resourceGroup\>* \(in the example, `default` is used\)


    
    </td>
    </tr>
    </table>
    
5.  Send the request.

     ![](images/List_Configurations_with_Postman_86c3ebb.png) 




<a name="loio8074b2a206cb41a2a68ba149a2150ea1__section_a2q_fps_ppp"/>

## Using curl

```
curl --request GET "[/pandoc/div/div/horizontalrule/codeblock/span/code
     {"filepath"}) $AI_API_URL/v2/lm/configurations (code]" --header "Authorization: Bearer $TOKEN" --header "ai-resource-group: $RESOURCE_GROUP"
```

> ### Output Code:  
> ```json
> {
>    "count":2,
>    "resources":[
>       {
>          "createdAt":"2021-02-04T11:50:45Z",
>          "executableId":"pytf-training",
>          "id":"1e6c2a5f-eabe-49a2-88e7-887145a2ef88",
>          "inputArtifactBindings":[
>             {
>                "artifactId":"521f7f17-876e-4369-9162-09748b56d27a",
>                "key":"churn-data"
>             },
>             {
>                "artifactId":"521f7f17-876e-4369-9162-09748b56d27a",
>                "key":"textclass-data"
>             }
>          ],
>          "name":"pytf-demo-config1",
>          "parameterBindings":[
>             {
>                "key":"train-epoch",
>                "value":"100"
>             }
>          ],
>          "scenarioId":"84fe6957-1145-4183-b682-8f11ca56d060"
>       },
>       {
>          "createdAt":"2021-02-04T11:59:22Z",
>          "executableId":"pytf-training",
>          "id":"42147d0d-5e3a-424d-a3a1-545b842379c5",
>          "inputArtifactBindings":[
>             {
>                "artifactId":"521f7f17-876e-4369-9162-09748b56d27a",
>                "key":"churn-data"
>             },
>             {
>                "artifactId":"521f7f17-876e-4369-9162-09748b56d27a",
>                "key":"textclass-data"
>             }
>          ],
>          "name":"pytf-demo-config2",
>          "parameterBindings":[
>             {
>                "key":"train-epoch",
>                "value":"1"
>             }
>          ],
>          "scenarioId":"84fe6957-1145-4183-b682-8f11ca56d060"
>       }
>    ]
> }
> ```

**Parent topic:** [Train Your Model](train-your-model-a9ceb06.md "You execute a training workflow to train your AI learning model.")

**Related Information**  


[Choose a Resource Plan](choose-a-resource-plan-57f4f19.md "You can configure SAP AI Core to use different infrastructure resources for different tasks, based on task demand. SAP AI Core provides several preconfigured infrastructure bundles called “resource plans” for this purpose.")

[Workflow Templates](workflow-templates-83523ab.md "Here, you can find a minimal workflow example template, that can be adapted to meet the requirements of your workflow.")

[List Scenarios](list-scenarios-deedde5.md "A scenario is a group of related executables for a use case within the user's tenant. A scenario can have multiple versions that further correspond to the different versions of executables.")

[List Executables](list-executables-80895a4.md "An executable is a template that is instantiated for a purpose, such as training a model or creating a deployment. You can list all of the executables in a scenario and get details of specific executables from a scenario. Workflow templates are mapped to training executables.")

[Create Configurations](create-configurations-884ae34.md "A configuration is a collection of parameters, artifact references, and executables that are used to run an execution or deployment.")

[Start Training](start-training-54b44e4.md "Start training and check the status of the execution.")

[Stop Training Instances](stop-training-instances-3d85344.md#loio3d853443027449d9a33723165b19b25a "")

[Delete Training Instances](delete-training-instances-612ce17.md#loio612ce172e609432a840a22eb211ecf7b "Deleting a training instance releases the SAP AI Core resources that it used.")

[Retrieve Execution Logs](retrieve-execution-logs-fbc55d3.md "Information about API processing and metrics, are stored and accessed in the deployment and execution logs.")

[Training Schedules](training-schedules-2b702f8.md "")

