LAB6 : Add Security Policy to API

#### Apply a Security Policy 

- Navigate back to the API Platform – Management Portal
- Open your API, CreateServiceOrg-NN
- Click on API Implementation
From the list on the right with Available Policies
- Under Security, select Key Validation

![API Platform](/images/40.png)

Configure as follows
- Leave first page as-is, click the “>”-icon¨
- Select Header
- Key Header: app-key
- Click Apply

![API Platform](/images/41.png)

Click Save
- Click on Deployments
- Re-deploy the API to the Gateway
- Open Postman
Test the POST-request again
- Note the Response

![API Platform](/images/42.png)

Add the key to the request
- In the request “Headers”
- Add key: app-key
- In the Value-section, paste your Application Key
Test again

