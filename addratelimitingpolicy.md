## LAB3: Add Rate Limiting Policy

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

