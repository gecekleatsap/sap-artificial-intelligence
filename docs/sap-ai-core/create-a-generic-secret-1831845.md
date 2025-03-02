<!-- loio1831845910364e97b3a7c6644a9e1f4b -->

# Create a Generic Secret

A generic secret gives SAP AI Core authorization to utilize your resource group without exposing your credentials.

SAP AI Core lets you optionally use generic secrets at two levels: at the main-tenant scope or on a resource-group level.

Generic secrets are different to system secrets \(such as object store, Docker registry, and so on\) and can be used to store sensitive information, either for the main tenant or for each resource group via an API. The latter can be attached to containers in executions or deployments as environment variables or volume mounts.

To create a generic secret in a resource group, send a POST request as shown below. Note that the API expects sensitive data to be Base64-encoded. You can easily encode your data in Base64 format using the following command on linux or macOS: `echo -n 'my-sensitive-data' | base64`



<a name="loio1831845910364e97b3a7c6644a9e1f4b__section_apy_mvk_4rb"/>

## Using Postman

1.  Create a new POST request and enter the URL ***\{\{apiurl\}\}/v2/admin/secrets***.
2.  As the request body, select the *raw* radiobutton and enter the following:

    ```
    {
    "name": "my-generic-secret",
    "data": {
    		"some-credential": "bXktc2VjcmV0LWNyZWRlbnRpYWw=",
    		"other-credentials": "bXktc2VjcmV0LW90aGVyLWNyZWRlbnRpYWw="
    		}
    }
    ```

    -   `name`: Set the name of your generic secret.
    -   `data`: Enter a JSON string that represents your generic secret.

3.  Specify the scope of the request via the header `AI-Tenant-Scope` or `AI-Resource-Group`:

    -   ***AI-Tenant-Scope*** : ***true***. The operation will be performed at the main tenant level.
    -   ***AI-Resource-Group*** : ****<resource-group-name\>****. The operation will be performed at the resource-group level.

    In this example, we are using the resource-group level.

    ![](images/AIHeader_ada6573.png)

4.  Send the request.

![](images/Create_Generic_Secret_in_Postman_06abf01.png)



<a name="loio1831845910364e97b3a7c6644a9e1f4b__section_l5m_rvk_4rb"/>

## Using curl

Submit a POST request to the endpoint `v2/admin/secrets` and include the name of your generic secret and credentials. Specify the scope through the `AI-Tenant-Scope` or `AI-Resource-Group`. The following code shows a request with the resource-group scope, indicated by `AI-Resource-Group: default`. For a creation request at main-tenant level, replace `AI-Resource-Group: default` with `AI-Tenant-Scope: true`.

```
curl --location --request POST "[/pandoc/div/div/horizontalrule/codeblock/span/code
     {"filepath"}) $AI_API_URL/v2/admin/secrets (code]" \
--header "Authorization: Bearer $TOKEN" \
--header 'Content-Type: application/json' \
--header 'AI-Resource-Group: default' \
--data-raw '{
	"name": "my-generic-secret",
	"data": {
		"some-credential": "bXktc2Vuc2l0aXZlLWRhdGE="
			}
}'					
```

**Parent topic:** [Manage Resource Groups](manage-resource-groups-8aae6cb.md "A resource group represents a unique workspace environment, where users can create or add entities such as configurations, executions, deployments, and artifacts.")

**Related Information**  


[Create a Resource Group](create-a-resource-group-01753f4.md "You can create resource groups to isolate ML workloads.")

[List All Generic Secrets](list-all-generic-secrets-05a3713.md "Locate a generic secret, without revealing sensitive information.")

[Update a Generic Secret](update-a-generic-secret-b5d5970.md "Generic secrets can be amended.")

[Delete a Generic Secret](delete-a-generic-secret-d5d5187.md "Manage the lifespan of your generic secrets.")

[Consume Generic Secrets in Executions or Deployments](consume-generic-secrets-in-executions-or-deployments-185a324.md "Utilize generic secrets in executions or deployments.")

