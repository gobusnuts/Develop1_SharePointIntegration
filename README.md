# Develop1_SharePointIntegration
Custom Sharepoint integration component for Microsof Dynamics 365 Customer Experince (CRM).

This repositry is based on the sample created by Scott Durrow (https://github.com/scottdurow)
The code was first published at https://code.msdn.microsoft.com/SharePoint-Integration-c5f21604
Read Scott's blog post for more information at http://develop1.net/public/post/SharePoint-Integration-Reloaded-e28093-Part-3.aspx

License: [MIT](http://www.opensource.org/licenses/mit-license.php)

# Introduction
In this sample I’ll show you how to integrate with SharePoint directly rather than relying on the out of the box integration. 
Using the standard integration, a new folder will be created for each record underneath the default site. In some solutions you’ll find that you want to modify this behaviour so that folders are created in a custom location. You may for example want to have an opportunity folder created under a site that is specific to a particular client rather than all under the same site.
The challenge with integrating with SharePoint using a CRM Online Workflow Activity/Plugin is that you can’t reference the SharePoint Assemblies which authenticating and calling the SharePoint web service somewhat harder. Thanks goes to fellow Dynamics CRM MVP Rhett for his blog that provided a starting point for this sample - https://bingsoft.wordpress.com/2013/06/19/crm-online-to-sharepoint-online-integration-using-rest-and-adfs/. The sample code in this post shows how to create a folder in SharePoint and then associate it with a Document Location. The authentication with SharePoint works via ADFS and since the out of the box integration uses a trust between CRM and SharePoint that is not accessible from a sandbox (even if you try and ILMerge it!) we have to provide a username and password that will act as our privileged user that can create folders in SharePoint. I have left a function where you can add your own credentials or implement a method to retrieve from a secure entity in CRM that only administrators have access to. Look in the code for the ‘GetSecureConfigValue’ function.
 
# Building the Sample
The workflow activity is deployed using the Developer Toolkit for Dynamics CRM and performs the following:
Description
The sample contains a custom workflow activity that works on both CRM Online and CRM OnPrem accepting the following parameters:
Site –  A reference to the site that you want to create a folder in. You could store a look up to a site for each customer and populate this parameter from the related account. 
Record Dynamic Url – The ‘Dynamic Record Url’ for the record that you want the SharePoint document location to be related to. This uses my Polymorphic input parameter technique. You simply need to pass the Record Url (Dynamic) for the record that you wish to create the folder for. 
Document Library Name – The name of the document location to create the folder underneath. In the out of the box integration this is the entity logical name (e.g. account) 
Record Folder Name – The name of the folder to create. You could use the client name, client ID etc. – but it will automatically have the GUID appended to it to ensure uniqueness just like the out of the box integration

# More Information
For more information see the original blog post - http://develop1.net/public/post/SharePoint-Integration-Reloaded-e28093-Part-3.aspx
