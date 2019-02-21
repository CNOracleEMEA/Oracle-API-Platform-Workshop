## Oracle API Platform Virtual Workshop Labs

This set of labs covers the following Oracle Services –
- Apiary – for API Design
- API Platform CS – for API Management


The use case is very simple – we need to be able to expose an API that allows us to create new organizations, we will start from the design of that API in the first part and in second part look into management of that API on exposure side.


### API Platform (API Design)

Apiary is the de facto tool for designing APIs. At this stage you should have been given access to Apiary.

•	Login to Apiary at http://apiary.io

•	Create a new API Project

![Apiary Project](/images/1.png)

•	Enter the name – NN-OrganizationService
NN being the number assigned to you by the trainers
-	Make sure to select Team API. 
-	Keep the format as API Blueprint. 

<a href="url"><img src="https://github.com/CNOracleEMEA/Oracle-API-Platform-Workshop/blob/master/images/2.png" align="left" height="500" width="300" ></a>


Your API project is created with default content – this default API is with Polls example –

![Apiary Project](/images/3.png)

- Copy and paste the definition below, replacing the example API with API that describes service that is supposed to create organization .

```
FORMAT: 1A
HOST: http://organizations.apiblueprint.org/

# OrganizationService

OrganizationService is an API for managing your Service Cloud Organizations

## Organizations Collection [/organization]


### Create an Organization [POST]


+ Request (application/json)

        {
            "orgName": "Beverages1",
            "contactFirstName": "Chris",
            "contactLastName": "O'Connor",
            "contactEmail": "cc@hotd.ie",
            "country": "IE"            
        }

+ Response 201 (application/json)

    + Headers

            Location: /organization/2

    + Body

            {
                "orgId": "123",
                "status": "New Org Created"
            }

```

You should now have an API definition which looks like this:

![Apiary Project](/images/4.png)

-	Click Save
Note the 2 panels – the definition on the left in API Blueprint – the more documentary version on the right.

-	Click on “Create an Organization” in the right panel.

![Apiary Project](/images/5.png)

Apiary comes with its own “mock” server, which “hosts” the APIs. This allows us to test the API.

•	Note the URL at the top – should look something like this:

```
https://private-af8f44-01organizationservice.apiary-mock.com/organization
```

Also note the multi-programming language support.

•	Next to Mock Server - Select cURL and click Try. 

![Apiary Project](/images/6.png)

•	Click Call Resource 

![Apiary Project](/images/7.png)

This should prompt a response like this:

![Apiary Project](/images/8.png)

So now we have our API contract, we also have a stub that a mobile developer could use to start developing a mobile app, while we now look at implementing this API in OIC.


### API Platform 

•	Login to API Platform – Management Portal
	Use your trial account
•	Click on APIs tab on the top left corner

![API Platform](/images/9.png)

•	Click on Create API on the top right corner

![API Platform](/images/10.png)

•	Enter CreateServiceOrg-NN as API name and 1.0 as version. Select ‘Create a default plan for this API’

![API Platform](/images/11.png)

![API Platform](/images/12.png)

#### Change API Request Policy

If not open already, open your API
- Click API Implementation 
- Click API Request Policy 
- Click Edit

![API Platform](/images/13.png)

- Under API Request URL enter OrganizationNN
- Click Apply

![API Platform](/images/14.png)

#### Deploy the API to a Gateway

Now we will deploy the API to a Gateway. These can run anywhere – on-premise, in the Oracle cloud, in any other cloud.
- Click on Deployments

![API Platform](/images/15.png)

- Click Deploy API

![API Platform](/images/16.png)

Configure as follows

- Development Gateway is checked
- Initial Deployment State: Active

Click Deploy

![API Platform](/images/17.png)

Note that the number of API’s waiting (n) for deployment is incremented before the number of Deployed (n) is incremented.
- Verify that new Gateway was deployed

![API Platform](/images/18.png)

#### Test the API in Postman

Now let’s test the API – using Postman (or similar program)
- Navigate back to your API. Remember the newly deployed gateway. Copy the associated URL

![API Platform](/images/19.png)

In Postman, open a new Request-tab
- Enter the URL you copied 
- Add “/createOrg” to the end of the URL (remember the API-design)
- Make sure you are using a POST-call
- Under the tab Authorization
- Type: Basic Auth
- Enter your OIC credentials

![API Platform](/images/20.png)

Click on the Body-tab
- Choose “raw”s
- Select “JSON(application/json)”
- Enter the request payload 

```
{ "orgName": "Bevarage1", "contactFirstName": "Chris", "contactLastName": "O'Connor", "contactEmail": "cc@hotd.ie", "country":"IE" }
```
- Click Send

You should have a response similar to this:

![API Platform](/images/21.png)

#### Add a Policy

Now you will add the a policy to regulate Traffic in the API.
- Open your API
- Select API Implementation
- From the list on the right-hand side “Available Policies”, expand Traffic Management
- Click Apply on “API Rate Limiting” 

![API Platform](/images/22.png)

Configure as follows
- Policy name: Leave as-is (API Rate Limiting)
- Place after the following policy: As-is (API-Request)
- Click next ( “>”-icon )
- Allow API Rate Limiting: per Logical Gateway
- API Rate Limit: 4
- Time Interval: Minute

Click Apply

![API Platform](/images/23.png)

Click Save

![API Platform](/images/24.png)

Re-deploy to the Gateway

![API Platform](/images/25.png)


#### Create a Plan

We will now create a plan and add the API as an entitlement to this plan.

Click Plans on the left Menu and than click Create

![API Platform](/images/50.png)

Enter the following details
- Plan Name
- Version

Click Create button.

![API Platform](/images/51.png)

Now click on Entitlements icon and than Add Entitlements.

![API Platform](/images/52.png)

Select your API and click Add

![API Platform](/images/53.png)


#### Publish to the Developer Portal

Open your Plan

![API Platform](/images/27.png)

The API is listed in the plan, but needs to be published to be activated
- Click Entitlements
- Hover over Unpublished to make the choices visible
- Click Publish
- When prompted “Are you sure you want to publish this entitlement?” – click Yes

![API Platform](/images/28.png)

You can verify the results: 

![API Platform](/images/29.png)

Now we can publish the plan to the developer portal

- Click on Publication
- View the URL and ending, its own unique Vanity Name. A vanity name is the URI path of an API’s details page when it is published to the Developer Portal.

![API Platform](/images/30.png)

![API Platform](/images/31.png)

Once Published, you can unpublish, republish etc.

Let’s now deploy the API to the Developer Portal
- Once back in your API, CreateServiceOrg-NN, and click on Publication
- Click on the end of the API Portal URL to edit the unique name
- Click the check-mark to verify

![API Platform](/images/32.png)

- Click Publish to Portal

![API Platform](/images/33.png)

#### Check out the API in the Developer Portal

- Login to the API Platform - Developer Portal
Use your cloud trial account
- Identify your API in the list, filter by searching if needed
- Click on it

![API Platform](/images/34.png)

Note the embedded documentation from Apiary (only if Standard or Professional edition of Apiary is used).
- Click on Subscribe

![API Platform](/images/35.png)

- Click on Select Plan

![API Platform](/images/36.png)

APIs are used in the context of an Application, e.g. a mobile app the developer is working on.

- Click Create New Application

![API Platform](/images/37.png)

- Enter your app name etc.
- Click Save

![API Platform](/images/38.png)

- Note the Application Key, copy it for later
- Click Subscribe

![API Platform](/images/39.png)

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

























































