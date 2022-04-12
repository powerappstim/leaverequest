<h1 align="center">Leave Request Template</h1>

<div align="center">
  An enhanced version of the built in Power Apps leave request template.
</div>

## Introduction

A very popular built-in template in Power Apps is the "leave request template".

This is a great template and there are two feature requests that app-builders frequently ask for. 
These are:

- To modify the template so that it works with a **SharePoint** data source instead of Excel.
- To enable the creation of **half-day** leave requests

For app builers who require this functionality, this project contains a modification of the template with these two features added.

## Getting started
A prerequisite step is to create a set of supporing SharePoint lists. We can create the SharePoint lists manually or we can create a SharePoint site and lists with PowerShell.

### Manual installation.
To create the SharePoint lists manually, create the following 3 lists:

#### Balance
<table>
<tr><td>EmployeeEmail</td><td>Single line of text</td></tr>
<tr><td>EmployeeName</td><td>Single line of text</td></tr>
<tr><td>Year</td><td>Single line of text</td></tr>
<tr><td>Vacation</td><td>Number</td></tr>
<tr><td>VacationUsed</td><td>Number</td></tr>
<tr><td>Sick</td><td>Number</td></tr>
<tr><td>SickUsed</td><td>Number</td></tr>
<tr><td>Floating</td><td>Number</td></tr>
<tr><td>FloatingUsed</td><td>Number</td></tr>
<tr><td>JuryDuty</td><td>Number</td></tr>
<tr><td>JuryDutyUsed</td><td>Number</td></tr>
<tr><td>Bereavement</td><td>Number</td></tr>
<tr><td>BereavementUsed</td><td>Number</td></tr>
<tr><td>BalanceID</td><td>Single line of text</td></tr>
<tr><td>Modified</td><td>Date and Time</td></tr>
<tr><td>Created</td><td>Date and Time</td></tr>
<tr><td>Created By</td><td>Person or Group</td></tr>
<tr><td>Modified By</td><td>Person or Group</td></tr>
</table>
  
#### Holidays
<table>
<tr><td>HolidayName</td><td>Single line of text</td></tr>
<tr><td>StartDate</td><td>Date and Time</td></tr>
<tr><td>Modified</td><td>Date and Time</td></tr>
<tr><td>Created</td><td>Date and Time</td></tr>
<tr><td>Created By</td><td>Person or Group</td></tr>
<tr><td>Modified By</td><td>Person or Group</td></tr>  
</table>

#### Leave
<table>
<tr><td>Title</td><td>Single line of text</td></tr>
<tr><td>Detail</td><td>Single line of text</td></tr>
<tr><td>StartDate</td><td>Date and Time</td></tr>
<tr><td>StartDatePartialType</td><td>Number</td></tr>
<tr><td>EndDate</td><td>Date and Time</td></tr>
<tr><td>EndDatePartialType</td><td>Number</td></tr>
<tr><td>LeaveType</td><td>Single line of text</td></tr>
<tr><td>Requester</td><td>Single line of text</td></tr>
<tr><td>Approver</td><td>Single line of text</td></tr>
<tr><td>Status</td><td>Single line of text</td></tr>
<tr><td>LeaveID</td><td>Single line of text</td></tr>
<tr><td>Modified</td><td>Date and Time</td></tr>
<tr><td>Created</td><td>Date and Time</td></tr>
<tr><td>Created By</td><td>Person or Group</td></tr>
<tr><td>Modified By</td><td>Person or Group</td></tr>  
</table>  

### PowerShell installation.
To create a SharePoint site with the 3 lists, download the [template file](LeaveRequestLists.xml) here and save it locally.

Next, apply the template with the PnP Framework and Provisioning Engine.

```bash
#1 - Connect to the destination SharePoint site 
Connect-PnPOnline -Url "https://destinationSite.sharepoint.com/sites/destinationSite" 

#2 - Import the items from the template file
Invoke-PnPSiteTemplate -Path "C:\PowerApps\SharePoint\leaveRequestTemplate.xml"

```

For additional help on how to install and to use the PnP Framework and Provisioning Engine, you can refer to the following blog post.

http://powerappsguide.com/blog/post/moving-sharepoint-sites-and-lists

### Additional steps

The leave request template is designed for users to submit vacation request for manager approval. Therefore, it's necessary to specify the manager for users in Microsoft 365. Microsoft 365 administrators can configure this through the admin portal here:

https://admin.microsoft.com

## Installing the app
To set up the app, you can import the [package file](LeaveRequestPackage.zip) or open the [MSAPP file](LeaveRequest.msapp) in Power Apps Studio.

Next, modify the data sources in the app to point to the SharePoint lists that were created in the pre-requisite step. You can then save and publish the app.

## How the app looks at one time
When a user makes a request leave, there is an option to select a partial start date through a drop down. The available options are "All day", "First half", and "Second half". 

![](docs/pic1.png?raw=true)

If the user chooses the "First half" start date option, the ability to select a partial end date is disabled.

![](docs/pic2.png?raw=true)

If the user selects the "All day" or "Second half" start options, there is the ability to select the partial end date types "All day" or "First half".

![](docs/pic3.png?raw=true)




