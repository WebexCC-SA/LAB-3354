## Create an New Repository In Your Personal GitHub Account
> Log into your [GitHub Account](https://github.com){:tatget="_blank"}  
> ??? note w50 "In the upper right corner , click on the `+` menu then select New Repository"
    ![](assets/newRepo.gif)
> Fill in the details:  
>> Repository Name: <copy>Wx1-Web-Components</copy>  
>> Choose visibility: Public  
>> Add README: False  
>> Add .gitignore: No .gitignore  
>> Add license: No License  
>
> Click Create repository  
> 
> ---

<form id="info">
<label for="info">Enter your GitHub Account Information</label><br>
  <label for="gh">GitHub Account:</label>
  <input type="text" id="gh" name="gh"><br>
    <label for="ghEmail">GitHub Email Address:</label>
  <input type="text" id="ghEmail" name="ghEmail"><br>
  <button onclick="setValues()">Update Lab Guide</button>
</form>

## Update the .gitignore file
> Open the .gitignore file in your project  
> Comment out `dist` (line 11) by placing your cursor on the line and using the keyboard shortcut using ctrl + /  
> Save the file (ctrl + s)  
> ---

## Update Git settings on the lab PC
> In the terminal of VS Code enter the following commands one at a time:  
> <copy>git config user.email "<w class="ghEmail"><w/>"</copy>  
> <copy>git config user.name "<w class="gh"><w/>"</copy>
>
> ---


## Remove the Current Remote Upstream Repository and Replace With Your New Repository
> In the terminal of VS Code enter the following commands one at a time:  
> <copy>git remote remove origin</copy>  
> <copy>git remote add origin https://github.com/<w class="gh">{githubAccount}</w>/Wx1-Web-Components.git</copy>  
> 
> ---


## Push Your Code
> In the terminal of VS Code enter the following commands one at a time:  
> <copy>git add .</copy>  
> <copy>git commit -m "My First Commit"</copy>   
> <copy>git push -u origin main</copy>  
>
> ---


## Option 1: Using Github Pages
> 


## Option 2: Using JSDelivr

## Update You Desktop Layout JSON to Use the Hosted Version of your Web Components

### Remove your Credentials from the lab PC

