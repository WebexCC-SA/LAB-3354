## Story
> As a contact center developer, I want to integrate Webex Contact Center SDK capabilities into a custom CRM application, so that agents can handle calls directly within their familiar business interface without switching between multiple applications.

!!! abstract w50 "Requirements"
    1. SDK Integration:
        - Initialize Webex Contact Center SDK with OAuth authentication
        - Register agent profile and retrieve available teams and login options
        - Handle agent login/logout operations
    2. Call Handling: 
        - Receive incoming call events and display call details
        - Provide call control functions (hold, resume, end)
        - Handle wrap-up codes and call completion
    3. CRM Integration:
        - Automatically search customer records when calls arrive
        - Display caller information and call associated details
    4. Real-time Updates:
        - Listen for agent state changes and task events
        - Update UI dynamically based on call status
        - Provide visual feedback for all operations

## Data and Actions

### Set up the development environment
> Create a new folder for your CRM banking application:  
> <copy>mkdir crm_bank_app && cd crm_bank_app</copy>  
> From terminal clone the repository containing the SDK implementation:  
> <copy>git clone https://github.com/shrishailsd/WX12025 .</copy>  
>
> ---

### Review the project structure and key files
> Open the project in VS code and examine the three critical files:
> > **banking-crm.html** - Contains the HTML structure for the CRM application  
> > **crm-app.js** - Handles CRM functionality and customer data management  
> > **wx1-sdk.ts** - Implements Webex Contact Center SDK integration  
>
> Navigate to line 194 in `banking-crm.html` to see how the LitElement web component is integrated:
> ??? note w50 "LitElement Integration Example"
    ```html
    <wx1-sdk accesstoken="${accessToken}"></wx1-sdk>
    ```
>
> ---

### Examine the SDK implementation architecture
> Open `wx1-sdk.ts` and review the class structure and key methods:
> > **@customElement("wx1-sdk")** - Defines the custom web component  
> > **@property({ reflect: true }) accesstoken** - Access token property binding  
> > **@state()** decorators - Component state management  
> > **startConnection()** - Initializes Webex SDK connection  
> > **getOptions()** - Sets up agent options and event listeners  
> > **actionTask()** - Handles call control operations  
>
> ??? question w50 "What SDK methods are being used for call handling?"
    - `this.webex.cc.register()` - Register agent profile
    - `this.webex.cc.on()` - Listen for events
    - `task.hold()`, `task.resume()`, `task.end()` - Call controls
    - `task.wrapup()` - Complete call with wrap-up reason
>
> ---

### Install dependencies and run the setup script
> Execute the setup script from terminal to check prerequisites and install dependencies:  
> <copy>./setup.sh</copy>  
> This script will:
> > - Verify Node.js installation  
> > - Install required npm packages  
> > - Set up TypeScript compilation  
> > - Configure the development server  
>
> ---

## SDK Authentication and Initialization

### Obtain and configure your access token
> Navigate to the [Webex Developer Portal](https://developer.webex.com/){:target="_blank"} and login using your agent credentials. On the right side top click on the avatar and copy the bearer token.  
> 
> In the CRM application interface, locate the access token input field  
> Paste the token you copied.
> 
> ---

### Initialize SDK connection and retrieve agent profile
> Click the "connect" button to initialize the SDK connection  
> The system will automatically:
> > - Validate your access token  
> > - pulls your desktop profile 
> > - Load available teams and login options 
>
> ??? challenge w50 "What information is retrieved during agent registration?"
    The profile object contains:
    - Agent name and ID
    - Available teams
    - Voice login options (BROWSER, AGENT_DN, etc.)
    - Idle codes and wrap-up codes
    - Dial number assignments
>
> ---

### Agent login process
> From the loaded profile information:
> > Select your assigned team from the dropdown  
> > Choose **AGENT_DN** as the login option  
> > Select your provided dial number: <copy><w class="dn">your-assigned-dn</w></copy>  
> > Click "Login" to establish your agent session  
>
> ---

## Call Handling Implementation

### Understanding the event-driven architecture
> The SDK uses an event-driven pattern for real-time updates:
> ??? note w50 "Key Event Listeners"
    ```typescript
    // Agent state changes
    this.webex.cc.on("AgentStateChangeSuccess", (event) => {
        // Handle idle code updates
    });
    
    // Incoming calls
    this.webex.cc.on("task:incoming", (task) => {
        // Process new call data
    });
    
    // Call completion
    this.task.once("task:end", (task) => {
        // Handle wrap-up selection
    });
    ```
>
> ---

### Test incoming call handling
> Place a test call to your assigned number: <copy><w class="dn">your-test-number</w></copy>  
> Observe the automatic processes:
> > - Call details populate in the SDK component  
> > - ANI (caller number) is extracted and displayed  
> > - CRM automatically searches for customer records  
> > - Call control buttons become available  
>
> ??? challenge w50 "How does the CRM integration work with incoming calls?"
    ```typescript
    this.webex.cc.on("task:incoming", (task) => {
        this.ani = task.data.interaction.callAssociatedDetails.ani;
        // Automatically trigger CRM customer search
        this.callCrmSearch(this.ani);
    });
    ```
>
> ---

### Implement call control operations
> Test each call control function during an active call:
> > **Hold** - Temporarily pause the call  
> > **Resume** - Reactivate a held call  
> > **End** - Terminate the call and initiate wrap-up  
>
> ??? question w50 "What happens when you end a call?"
    The system automatically presents a wrap-up code selection interface, requiring the agent to categorize the call before becoming available for new calls.
>
> When a call ends, the wrap-up selection interface appears:
> ??? note w50 "Wrap-up Implementation"
    ```typescript
    handleWrapupSelection(e: any) {
        const selectedValue = e.target.value;
        const selectedOption = e.target.selectedOptions[0];
        
        if (selectedValue && selectedOption) {
            const wrapupName = selectedOption.dataset.name;
            this.actionTask("wrapup", selectedValue, wrapupName);
        }
    }
    ```
> Select an appropriate wrap-up reason from the dropdown  
> The call will be completed and you'll return to available status  
>
> The SDK automatically tracks and responds to agent state changes:
> > - Login/logout events  
> > - Available/Idle events.
>
> ??? challenge w50 "How can you extend this to add custom state monitoring?"
    Add additional event listeners for specific state changes:
    ```typescript
    this.webex.cc.on("AgentStateChange", (event) => {
        // Custom state change handling
        console.log("Agent state changed:", event);
    });
    ```
>
> ---

## Testing and Validation

### Comprehensive call flow testing
> From the terminal run 'npm run dev', this will spin up your application automatically in the browser.
> Before testing, you need to configure the CRM with your phone number for automatic customer lookup:
> Open `crm-app.js` and edit the customer record from line 40 with your details:
> ??? note w50 "Update Customer Record"
    ```javascript
    '1': {
        id: '1',
        firstName: 'john',         // Your FirstName
        lastName: 'smith',         // Your lastName
        phone: '(555) 987-6544',  // Replace with your ANI
        email: 'john.smith@email.com',
        address: '123 Main St, Anytown, ST 12345',
        dob: '1985-06-15',
        memberSince: '2020-03-10',
        notes: 'Preferred customer, has premium account package.'
    }
    ```
> Replace the firstName, lastName and phone number (the number you'll be calling from)
>
> Perform end-to-end testing of the complete call workflow:
> > 1. Place an inbound call: <copy><w class="dn">test-number</w></copy>  
> > 2. Verify automatic customer lookup in CRM displays your updated record  
> > 3. Test all call control functions (hold, resume)  
> > 4. End the call from the phone you dialed in and complete wrap-up  
> > 5. Confirm return to available status  
>
> ---

### Advanced testing with browser console
> Launch the browser console to observe SDK event logs during testing:
> > Open browser Developer Tools (F12)  
> > Navigate to the Console tab  
> > Repeat the call flow test from above  
> > Observe the SDK event logs, Filter console logs with [WX1-SDK] to see SDK related logs and [BANKING-CRM] to see CRM related logging.
> > Review the source code implementation during testing based on logs.
>
> Test the logout functionality:
> > Click the 'Logout' button in the SDK component  
> > Ensure you are returned to the home screen 
>
> ---