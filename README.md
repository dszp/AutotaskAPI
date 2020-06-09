
# AutotaskAPI PowerShell Module

  

This is a PowerShell wrapper for the new Autotask REST API released by Datto in version 2020.2. This API is a replacement of the SOAP API.


# Installation instructions

  

This module will be published in the PowerShell gallery. The future installation command will be

    install-module AutotaskAPI.

# Usage

To get items using the Autotask API you'll first have to add the authentication headers using the` Add-AutotaskAPIAuth` function.  Example:

    Add-AutotaskAPIAuth -username 'YourUsername@YourDomain.com' -secret 'ThePasswordToYourUser' -ApiIntegrationcode 'ABCDEFGH00100244MMEEE333'
When the command runs, we will try to decide the correct webservices URL for your zone based on the e-mail address. If this fails you must manually set this:

    Add-AutotaskBaseURI -BaseURI https://webservices1.autotask.net/atservicesrest
The Base URI value has tab completion to help you find the correct one easily.

To find resources using the API, execute the `Get-AutotaskAPIResource` function. For the `Get-AutotaskAPIResource` function you will need either the ID of the resource you want to retrieve, or the JSON SearchQuery you want to execute. 

**Examples:**
To find the company with ID 12345:

    Get-AutotaskAPIResource -Resource Companies -ID 12345
 To get all companies that are Active:
 
    Get-AutotaskAPIResource -Resource Companies -SearchQuery "{filter='active -eq True'}"

To create a new company, we can either make the entire JSON body ourselves, or use the `New-AutotaskBody` function.

    $Body = New-AutotaskBody -Definitions CompanyModel
  This creates a body for the model Company. Definitions can be tab-completed. The body will contain all expected values. If you want an empty body instead use:

    $Body = New-AutotaskBody -Definitions CompanyModel -NoContent

After setting the values for the body you want, execute:

    New-AutotaskAPIResource -Resource Companies -Body $body
To set exisiting companies, use the `Set-AutotaskAPIResource` function. This uses the Patch method so remember to remove any properties you do not want updated.

    Set-AutotaskAPIResource -ID -Body $body

# Contributions
Feel free to send pull requests or fill out issues when you encounter these.