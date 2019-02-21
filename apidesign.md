Apiary is the de facto tool for designing APIs. At this stage you should have been given access to Apiary.

•	Login to Apiary at http://apiary.io

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
