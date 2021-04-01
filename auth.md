# OneConsultation Authentication Flow

OneConsutation uses an authentication process to limit who can access the Admin Portal to see users who are waiting for an consultation, and to enable them to begin the consultation process.

This page describes that authentication process.

## High Level Summary

As part of the initial on-boarding process, a OneConsultation Azure Active Directory application is installed in your Azure tenant. This means that we can use Azure AD to “prove” that someone is a user from your domain and grant them access, without requiring them to enter another set of credentials. 

In order for this to work, you need to consent that our application can use your AD tenant for this purpose. **This is a common security practice and is the recommended Microsoft approach for securing SaaS applications in Azure.** There is a good high-level example walkthrough here: <https://docs.microsoft.com/en-us/azure/architecture/multitenant-identity/>

The actual permissions we ask for and use allows us to know that authentication was successful, the ID of the Office 365 Tenant, the ID of any AD Groups you are a member of (we do not see the group names), and the ability to create Teams Meetings. This is all we need to verify that a user is authorized and to place them into the correct tenant. We do not ask for, or have access to, any more detailed AD/user data, nor access to any Graph API data.  (If you’ve ever used a “sign in with Google”, “connect with Facebook” etc to log into other sites that aren’t Google/Facebook, this is the same process).
At any time, this application can be removed from your Azure application list and permission revoked. In addition, Azure provides a level of reporting around access and usage of the application that you can find information on [here](https://docs.microsoft.com/en-us/azure/active-directory/reports-monitoring/concept-usage-insights-report).

## Technical Detail

We have a multi-tenant Azure AD application, which requires admin consent before it can read  AD data for authentication. The security model we use is based on the flow here: <https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-authentication-scenarios> (specifically the section on Multi-tenanted Applications). 

From <https://docs.microsoft.com/en-us/azure/active-directory/develop/consent-framework>: *The Azure AD consent framework makes it easy to develop multi-tenant web and native client applications. These applications allow sign-in by user accounts from an Azure AD tenant, different from the one where the application is registered…the framework is based on a user or an administrator giving consent to an application that asks to be registered in their directory, which may involve accessing directory data. For example, if a web client application needs to read calendar information about the user from Office 365, that user is required to consent to the client application first. After consent is given, the client application will be able to call the Microsoft Graph API on behalf of the user, and use the calendar information as needed.…The consent framework is built on OAuth 2.0 and its various flows, such as authorization code grant and client credentials grant, using public or confidential clients. By using OAuth 2.0, Azure AD makes it possible to build many different types of client applications, such as on a phone, tablet, server, or a web application, and gain access to the required resources.*

An administrator can provide consent for all users in the tenant, meaning that each user is not presented with their own consent box – this is a favourable user experience.

To grant this access, visit this URL and authenticate as a Office 365 Admin: <https://login.microsoftonline.com/common/oauth2/authorize?resource=https://graph.windows.net&response_type=code&client_id=5637a6d7-9ce0-4788-b498-e96008b4ccb9&redirect_uri=https://admin.oneconsultation.net&scope=openid&prompt=admin_consent>

You’ll see a box similar to this:

![alt text](https://raw.githubusercontent.com/modalitysystems/oneconsultation-docs/master/images/auth/1.png "Azure AD Admin Consent")

You’ll notice that Azure explicitly lists out the permissions which you are granted to this application, which are minimal and designed so that we can verify the identity of the user, and the tenant ID. You should review the permissions and once you are happy, click Accept. This will grant the application those permissions until they are revoked. 

Once you have done this, the application is listed as an Enterprise Application in your Azure Portal. At any time you can review the list of applications with permission in your Azure tenant using the Portal. Here’s an example of OneConsultation installed in a test tenant:

![alt text](https://raw.githubusercontent.com/modalitysystems/oneconsultation-docs/master/images/auth/2.jpg "OneConsultatino AD Application")

From here you can monitor usage, review permissions and remove the application which will revoke the permission.

## Permissions

During the Admin Consent process, you will be shown the permissions which OneConsultation is requesting. They are:

 - Read directory data
 - Sign in and read user profile
 - Access the directory as the signed-in user
 - Read and create online meetings (application scope, not user user)

These permissions allow us to read the profile of the signed-in user and gives us the same access to data in AD as the signed-in user.

The intent behind the permissions request is:

 - Reading the tenant ID of the signed-in user (to enable us to route you to the correct consultation rooms)
 - Reading the list of groups a user is a member of (to restrict access based on AD group)
 - To create Teams Meetings (future functionality)


There’s more detail about the permissions scopes here, which provides a summary of the permissions and the description:
<https://msdn.microsoft.com/library/azure/ad/graph/howto/azure-ad-graph-api-permission-scopes>.










