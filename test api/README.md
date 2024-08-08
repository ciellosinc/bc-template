# Testing Templates in Postman and REST Client
In this project you can find Testing Templates in Postman and REST Client for API, OData and SOAP endpoints.

## Setting up variables and fields

To use Postman and REST Client templates it is necessary to set variables according to your tenant, environment and app registration.

You can find the Tenant and Environment Name in the Admin Center of Business Central.  

To work with REST Client and Postman it is necessary to setup an Authorization. It is recommended by Microsoft to use the OAuth 2.0 authorization protocol.

The following will describe the steps to obtain the data required for this type of authentication.

1. Sign in to **Microsoft Entra Admin Center** (https://entra.microsoft.com/#home)
2. Register an application for Business Central: Identity > Applications > App Registrations > New Registration and define: 
   - Name
   - Supported account types: Accounts in this organizational directory only (Contoso only - Single tenant) 
   - Redirect URI web = https://businesscentral.dynamics.com/OAuthLanding.htm 
   - Register the application and save the Application Id Client.
3. Create a secret in Certificates & secrets > New client secret > Add description + duration > Add.
   - Save the Secret VALUE.
4. Register the Grants in API permissions > Add a permission > Microsoft APIs > Dynamics 365 Business Central. 
   - Assign - API.ReadWrite.All and Automation.ReadWrite.All  
   - Consent of Grant Admin in Grant admin consent for.
5. In **Business Central** access Microsoft Entra applications, click in New and define:
   - Client Id = Application client Id.  
   - Set a description.
   - State = Enabled.  
   - Sign a permission.

## REST Client ins VSCode

To work with REST Client in VSCode it is necessary to install the Extension: REST Client.

REST Client allows you to send HTTP request and view the response in Visual Studio Code directly.

## REST Client API

In VSCode you need to set the variables:

- clientid = It is the Application Id defined in the Microsoft Entra Admin Center when you create a New Application.
- clientsecret = It is the Secret Value defined in the Microsoft Entra Admin Center when you create a New Application.
- scope = https://api.businesscentral.dynamics.com/.default
- tenant = Define your tenant Id
- environmentName = Define your Environment Name
- aPIPublisher = Define your API Publisher
- aPIGroup = Define your API Group
- aPIVersion = Define your API Version
- @baseAPIUrl =  {{baseUrl}}/v2.0/{{environmentName}}/api/{{aPIPublisher}}/{{aPIGroup}}/{{aPIVersion}}

After you define the variables, you can Send Request in the tokenrequest. Then you will have your token authenticated.

After creating the token you can run each necessary request.

Note: 

- If you want to use companyId in this format = {{companies.response.body.value[0].id}} you need to first Send Request GET companies then after you can use the others endpoints.
- Another possibility is to define the companyId as a variable in the at the beginning of the file.

## REST Client OData v.4

In VSCode you need to set the variables:

- clientid = It is the Application Id defined in the Microsoft Entra Admin Center when you create a New Application
- clientsecret = It is the Secret Value defined in the Microsoft Entra Admin Center when you create a New Application
- scope = https://api.businesscentral.dynamics.com/.default
- tenant = Define your tenant Id
- environmentName = Define your Environment Name
- companyId = Define the GUID of the company you want to use in the endpoints
- baseODataUrl = {{baseUrl}}/v2.0/{{tenant}}/{{environmentName}}/ODataV4/Company('{{companyId}}')

After you define the variables, you can Send Request in the tokenrequest. Then you will have your token authenticated.

After creating the token you can run each necessary request.

Note: in the endpoints it is possible to use de CompanyName instead of CompanyId.

## REST Client SOAP

In VSCode you need to set the variables:

- clientid = It is the Application Id defined in the Microsoft Entra Admin Center when you create a New Application.
- clientsecret = It is the Secret Value defined in the Microsoft Entra Admin Center when you create a New Application
- scope = https://api.businesscentral.dynamics.com/.default
- tenant = Define your tenant Id.
- environmentName = Define your Environment Name.
- company Name = Define the name of the company you want to use in the endpoints.
- baseSoapUrl = {{baseUrl}}/v2.0/{{tenant}}/{{environmentName}}/WS/{{companyName}}

After you define the variables, you can Send Request in the tokenrequest. Then you will have your token authenticated.

After creating the token you can run each necessary request.

## Postman

To use Postman template you should import the json files to your workspace in Postman. To do it you have to click in the "Import" button next to your workspace name and then drop or select the json file, in this case: "Cronus App.postman_collection"
 
To set the authorization in the next step, and after perform the requests, you have to firstly set the variables. To set them click in the collection name, in this case "Cronus App", and click on the "Variables" tab. After each needed change that you make you should save the modifications.
 
After setting up variables, you need to set authorization to create a token with the neccessary fields. To do that you should click on the collection name, select the "Authorization" tab and follow the next steps (some of this fields as said are set on the variables tab in the collection):
1. Choose Authorization = Oauth 2.0.  
   - Token Name = “choose” 
   - Grant type = authorization code 
   - Callback URL = https://businesscentral.dynamics.com/OAuthLanding.htm 
   - Auth URL = endpoints  Authorization Endpoint v2 
   - Access token url = endpoints  oauth 2.0 token endpoint v.2 
   - Client Id = application (client) id 
   - Client secret = client Secret
   - Scope =  https://api.businesscentral.dynamics.com/.default 
2. Get New Access Token 
3. Use Token

Since the each request is inheriting authorization from parent, after creating the token you can use it and run each necessary request.

# Additional resources:

- [Wiki API] https://dev.azure.com/ciellos-bc/Wiki/_wiki/wikis/main.wiki/200/API
- [OAuth] <https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/webservices/authenticate-web-services-using-oauth>
- [OData] <https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/webservices/odata-web-services>
- [SOAP] <https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/webservices/soap-web-services>
- [API] <https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/webservices/api-overview>
- [Using Automation APIs in Business Central – Deep Dive - YouTube](https://www.youtube.com/watch?v=HtSru012lRA)
- [Introduction to automation APIs - Business Central | Microsoft Learn](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/administration/itpro-introduction-to-automation-apis)
- [Business Central Administration Center API - Business Central | Microsoft Learn](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/administration/administration-center-api)
- [Cloud Migration API Overview - Business Central | Microsoft Learn](https://learn.microsoft.com/en-us/dynamics365/business-central/dev-itpro/administration/cloudmigrationapi/cloud-migration-api-overview)