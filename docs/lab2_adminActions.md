## Story
> As a contact center administrator, I need to log out agents which have not logged out after their shift, so that the contact center reporting statistics are accurate. 

!!! abstract w50 "Requirements"
    1. Need a list of logged in agents which includes:
        - Agent name
        - Team name
        - Login time
        - Current Status
        - Last Activity time
    2. Need to be able to log out an agent

## Data and Actions

### Log into the Agent Desktop (so that you have data to query against)
> Launch the [Agent Desktop](https://desktop.wxcc-us1.cisco.com/){:target="_blank"}
>
> > Login: <copy><w>admin login</w></copy>  
> > Password: <copy><w>password</w></copy>  
> > Team: <copy><w>team</w></copy> 
> ---

### Use the Search API GraphQL Workbench to create the query for the Search API 
> Open the [Search API GraphQL Workbench](https://webexcc-sa.github.io/tools/gqlWorkbench/){:target="_blank"}
>
> > Use the Authorization Tool (Tools > Authorization)
> >> Login: <copy><w>admin login</w></copy>  
> >> Password: <copy><w>password</w></copy>
>>
>> ??? note w50 "Copy the authorization header into the environment variables"
    ![](assets/GQL_token.gif)
>
> > Set the URL: <copy>https://api.wxcc-us1.cisco.com/search</copy>
> 
> Open the Docs Panel 
> Click Query to see which fields are available  
> ??? question w50 "Which Fields are we going to use to find information about agents?"
    agentSession  
> Click on the blue text of the name of the field you want to use  
You can now see the Arguments and Fields available  
> ??? note w50 "Hover over the name of the fields you selected in the previous step at the top of the frame and the ADD QUERY button will appear, click it"
    ![](assets/addQuery_agentSession.gif)
> You now have a query template in the first pane of Altair     
> ??? note w50 "Delete the "has" section and all of its fields"
    ![](assets/removeHas_agentSession.gif)
> In the Arguments section of the query (top section):
>> Delete the lines for aggregation, aggregations, and aggregationInterval as we are not using aggregations in this query.  
>
> ??? question w50 "Based on the requirements listed above in the story, what fields do you need to return in your query?"
     - Agent name = agentName
     - Team name = teamName
     - Login time = startTime
     - Current Status = 
     - Last Activity time = 



### Use API to log out agents
> Navigate to the [Agent Logout API documentation](https://developer.webex.com/webex-contact-center/docs/api/v1/agents/logout){:target="_blank"}



??? question w50 "Do we have all of the data we need to to make the logout API call?"
    You will also need the agentID of the agent you want to log out.  
    > Add agentId to the GQL query fields


