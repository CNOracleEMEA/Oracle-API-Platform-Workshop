## Oracle API Platform Virtual Workshop Labs

This set of labs covers the following Oracle Services –
- Apiary – for API Design
- API Platform CS – for API Management


The use case is very simple – we need to be able to expose an API that allows us to create new organizations, we will start from the design of that API in the first part and in second part look into management of that API on exposure side.


### API Platform (API Design)

Apiary is the de facto tool for designing APIs. At this stage you should have been given access to Apiary.

•	Login to Apiary at http://apiary.io

    o	Your trainer will provide you with the credentials

•	Create a new API Project

![Apiary Project](/images/1.png)

•	Enter the name – NN-OrganizationService
NN being the number assigned to you by the trainers
-	Make sure to select Team API. 
-	Keep the format as API Blueprint. 

![Apiary Project](/images/2.png)

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

















