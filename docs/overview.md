<script type="module" src="https://webexcc-sa.github.io/LAB-3354/template_assets/js/index.js"></script>

# Overview

## Learning Objectives

This lab will give you an introduction to building Web Components (Desktop Widgets) to extend the functionality of the agent desktop as well as using the new Webex Contact Center SDK to integrate the contact center into a line of business tool.

## Disclaimer

Although the lab design and configuration examples could be used as a reference, for design related questions please contact your representative at Cisco, or a Cisco partner.

## Tools and Other Lab Requirements
In this lab we will be using:
<div class="grid" markdown>
!!! tool "Tools"
    Yarn  
    Vite + Lit  
    VS Code Extensions  
    GraphQL Workbench    
    JSON Path Finder  

!!! tool "Software Requirements (preinstalled in lab)"
    Node JS  
    Visual Studio Code  
    Git
    Postman
</div>

---

## Lab Access
In this lab we will be using Webex for making calls into the Contact Center and for viewing demos which will be shared by the instructor.  We will be using the same account for Admin and Agent activities in the Contact Center.  Your guide will reflect your specific environment variables, including login information, Channels, Queues, Teams, and assigned numbers in the steps of the actual lab as you progress.


> Login: <copy><w class="login">Provided by proctor</w></copy>
> 
> Password: <copy><w class="PW">Provided by proctor</w></copy>
>
> Webex Phone Number: <copy><w class="WxC">Provided by proctor</w></copy>
> 
> Assigned Inbound Channel Number: <copy><w class="dn">Provided by proctor</w></copy>
>
> Assigned Queue Name: <copy><w class="Queue">Provided by proctor</w></copy>
>
> Assigned Team name: <copy><w class="Team">Provided by proctor</w></copy>
>
> Assigned Desktop Layout Name: <copy><w class="layoutName">Provided by proctor</w></copy>

---

<!-- <lab-auth callbackUrl="https://webexcc-sa.github.io/LAB-3354/oauth/index.html"></lab-auth> -->

Token: <copy><w class="token"><lab-auth callbackUrl="https://webexcc-sa.github.io/LAB-3354/oauth/index.html"></lab-auth></w></copy>

## Getting Started

> Log into Webex on your PC:
>
> - Username: <copy><w class="login">Provided by proctor</w></copy>
> - Password: <copy><w class="PW">Provided by proctor</w></copy>
> 

---
> Log into [Webex Control Hub](https://admin.webex.com){:target="_blank"} in Chrome

> Login: <copy><w class="login">Provided by proctor</w></copy>
> 
> Password: <copy><w class="PW">Provided by proctor</w></copy>

---
### Testing your lab setup
> 1. Launch the [Agent Desktop](https://desktop.wxcc-us1.cisco.com/){:target="_blank"} and log in selecting the Desktop option for your Voice connection.
1. From the Webex App, dial <copy><w class="dn">Provided by proctor</w></copy>
      1. The call will be place in your queue without hearing a greeting message.
      2. You will hear the hold music until the call is answered
2. In the agent desktop, set your status to Available and answer the call.
      1. Confirm that you can hear audio being passed in both directions.
      2. Disconnect the call
      3. Select a Wrap-up Code
      4. Set your status to Meeting
3. In the agent desktop, click on the dial pad. ![](howToUse/assets/dialPad.png){style="width:1.5em"}
      1. Enter your Webex Phone Number: <copy><w class="WxC">Provided by proctor</w></copy> in the text box 'Enter number to dial'
      2. Click on dial icon at the bottom of the dial pad pop up ![](howToUse/assets/dialOut.png){style="width:1.5em"}  
      3. Answer the call on your agent desktop  
      4. After answering, you will receive a call to your webex app. answer it 
      5. Ensure there are no errors  
      6. Disconnect the call  
---
