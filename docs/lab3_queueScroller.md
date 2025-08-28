## Story
> As a contact center director, I want my agents to have scrolling text on their agent desktop with call queue statistics for calls which they are eligible to receive, so they can see them without looking at another screen.

!!! abstract w50 "Requirements"
    1. Queues the agent is eligible to receive calls from:
        - Queues which include the agent's team
        - Direct skilled queues where the agent's skills match
        - Agent assigned queues where the agent is assigned
    2. For all calls: 
        - List the queue name
        - List the number of calls
        - Show the longest wait time in queue
    3.  Queue statistics should scroll on the agent desktop
        - Data should update automatically

## Data and Actions

### List all queues assigned to the agent by the team they are logged into
> Navigate to the [List references for a specific Team API](https://developer.webex.com/webex-contact-center/docs/api/v1/team/list-references-for-a-specific-team){:target="_blank"}  
> Get your team ID from Control Hub  
> Click to run the request  
> Copy the cURL and import it into Postman
>
> ---

### List all skilled queues from which the agent can receive calls
> [List skill based Contact Service Queue(s)by user ID](https://developer.webex.com/webex-contact-center/docs/api/v1/contact-service-queues/list-skill-based-contact-service-queuesby-user-id){:target="_blank"}  
> Get your userId from Control Hub
> Click to run the request  
> Copy the cURL and import it into Postman
>
> ---

### List all queues in which the agent is directly assigned
> [List agent based Contact Service Queue(s)by user ID](https://developer.webex.com/webex-contact-center/docs/api/v1/contact-service-queues/list-agent-based-contact-service-queuesby-user-id){:target="_blank"}
> Using the same userId as the previous request  
> Click to run the request  
> Copy the cURL and import it into Postman
>
> ---

??? question w50 "Did you notice anything interesting about the API calls and responses?"
    - All three use the dame method (GET)
    - The returned JSON has nearly the same structure
    - All three calls are using the same headers
    - All three are using the same URL root
Keep Postman open as we will be using the information in a future step

---


### Use the Search API to retrieve the number of contacts and oldest contact createdTime for the queues which the agent is assigned
For this query you will be using aggregations and a compound filter to retrieve the queue statistics.  
> Open the [Search API GraphQL Workbench](https://webexcc-sa.github.io/tools/gqlWorkbench/){:target="_blank"}  

> === "If your previous session is still valid"
     Click the Add New button  
> === "If your previous session is no longer valid"
      Use the Authorization Tool (Tools > Authorization)
     > Login: <copy><w>admin login</w></copy>  
     > Password: <copy><w>password</w></copy>
    >
    ??? note w50 "Copy the authorization header into the environment variables"
        ![](assets/GQL_token.gif)
    Set the URL: <copy>https://api.wxcc-us1.cisco.com/search</copy>  
> Open the Docs pane and add the query for task using the ADD QUERY button  
> Remove the has section  
> Remove the intervalInfo section  
> Remove all fields in the tasks section except lastQueue and aggregation  
> After lastQueue add: <copy>{name}</copy>  
> After aggregation add: <copy>{name value}</copy>
> In the Arguments section of the query, remove the lines for aggregation and aggregationInterval  
> Click the suitcase icon and select Prettify  
> 
> ---

#### Creating the aggregations
An Aggregation can return a count, sum, average, max, min, or cardinality of a field along with a name you provide.  They can also have their own set of filters which can be used to further refine the data into the information you require.   
In their most basic form an aggregation is represented like: `{ field: "string", type: count, name: "string" }` inside an array.
They can be further bifurcated by having other fields in the query.  In our case we are going to slice our aggregations based on the lastQueue where they were assigned.  
> ??? challenge w50 "Create an aggregation to return the count of contact"  
    { field: "id", type: count, name: "contacts" }
    > We are returning the count of the task IDs and naming is "contacts"
> Replace the aggregating template example in the query with your new aggregation leaving the square brackets. Then press enter twice to move the closing square bracket down to make room for the next aggregation.
> ??? challenge w50 "Create an aggregation to return the min createdTime and name it oldestStart"
    { field: "createdTime", type: min, name: "oldestStart" }
> Add this aggregating directly below the one you just created.
> Prettify your query. 


#### Creating the compound filter



## Creating the Web Component

### Create a new Web Component
> Create a new file in the src directory named <copy>queue-scroll.ts</copy>
> 
> In the new file, type (not paste) littemplate
>
> Select the **Create LitElement Component With lit-html**
> 
> ---

### Create Properties for the required variables
> token  
> orgId  
> teamId  
> agentId  

### Create States for the required data elements
> Array of queues  
> queueFilter
> _timerInterval

### Create method


### Create method


### Update the render method

### Add to index.html

### Add CSS Styling

!!! blank ""
    ```CSS
                :host {
                display: flex;
                }
                .marquee-container {
                width: 30vw;
                height: 50px; /* Set a fixed height for the container */
                overflow: hidden; 
                border:solid;
                border-radius:25px;
                }

                .marquee {
                list-style: none; /* Remove default list styles */
                display:flex;
                padding: 0;
                margin: 0;
                height:100%;
                width:max-content;
                animation: scroll linear infinite;
                animation-duration: 10s;
                align-items:center;
                }
                .marquee li {
                display:flex;
                align-self:center;
                align-items:center;
                justify-content:center;
                flex-shrink:0;
                font-size:2rem;
                white-space:nowrap;
                padding: 0 1rem 0 1rem;
                }
                .marquee:hover{
                animation-play-state: paused;
    
                }

                @keyframes scroll {
                0% {
                    transform: translateX(0); /* Start position */
                }
                100% {
                    transform: translateX(-50%); /* End position (fully scrolled) */
                }
                }
    ```


### Add auto refresh functionality
> Connected callback  
> Disconnected callback  


### Add to Desktop Layout

## Testing