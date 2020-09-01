# Setting up OneConsultation

OneConsultation is a fully managed hosted service, so there's not a lot of time-consuming setup, no machines to configure and no client settings to roll out. 

# To start using OneConsultation (production or trial)

## Step 1: Contact us!

Before you can start using OneConsultation (even a trial) you need to contact us so that we can provision the service for you. Contact your Modality Systems Account Manager, or use the enquiry form on our main [website](https://modalitysystems.com/software/oneconsultation).

We will provide you with details of your portal address and a named point of contact to work with throughout the remaining setup steps. Typically the entire process, from telling us to having customer make test consultations takes up to 72 hours, provided Step 2 is completed promptly (see below).

## Step 2: find your Office 365 Tenant ID

Your Office 365 tenant ID is a globally unique identifier (GUID) that is different than your tenant name or domain. It's allocated to you by Microsoft and never changes.

We use your tenant ID when you authenticate with OneConsultation to work out which consultations to show you. Your tenant ID acts as a the "key" to showing you only consultations which are meant for your organisation, and hiding those consultations from any other OneConsultation user. We need to know your tenant ID before you can start using OneConsultation.

To find your tenant ID:

**Use the Azure AD portal**

Office 365 uses Azure AD to manage user accounts. You can find your tenant ID in the Azure AD portal. You'll need to be an Azure AD administrator. To find your Office 365 tenant ID in the Azure AD portal:

 1. Log in to Microsoft Azure as an administrator.
 2. In the Microsoft Azure portal, click Azure Active Directory.
 3. Under Manage, click Properties. The tenant ID is shown in the Directory ID box.

**Use Windows PowerShell**

You can use Windows PowerShell to find the tenant ID. You'll need the [Microsoft Azure PowerShell module](https://go.microsoft.com/fwlink/p/?LinkId=717444).

Open a Microsoft Azure PowerShell command window and run the following script, entering your Office 365 credentials when prompted.

```
Login-AzureRmAccount
```

Your tenant ID is listed in the output.

Once you have your tenant ID, provide it to us to activate your account.

## Step 3: Federate with us

Please federate your Microsoft Teams or Skype for Business environment with our bridging service by adding the domain **onecvideo.net**. This is a Modality Systems owned domain which hosts the bridging service that powers OneConsultation. Microsoft Teams or Skype for users will connect with endpoints that are hosted on this service and with SIP addresses that end @onecvideo.net.

## Step 4: Grant permission to our Azure AD application

As part of the initial on-boarding process, a OneConsultation Azure Active Directory application is installed in your Azure tenant. This means that we can use Azure AD to “prove” that someone is a user from your domain and grant them access, without requiring them to enter another set of credentials. You can find more information on this [here](https://modalitysystems.github.io/oneconsultation-docs/auth.html)

An administrator can provide consent for all users in the tenant, meaning that each user is not presented with their own consent box – this is a favourable user experience.

To grant this access, visit this URL and authenticate as an Office 365 Admin: [login.microsoftonline.com/common/oauth2/authorize?resource=https://graph.windows.net&response_type=code&client_id=5637a6d7-9ce0-4788-b498-e96008b4ccb9&redirect_uri=https://admin.oneconsultation.net&scope=openid&prompt=admin_consent](https://login.microsoftonline.com/common/oauth2/authorize?resource=https://graph.windows.net&response_type=code&client_id=5637a6d7-9ce0-4788-b498-e96008b4ccb9&redirect_uri=https://admin.oneconsultation.net&scope=openid&prompt=admin_consent)

### Once you have confirmed back to us that these setup steps are complete, we will provide you with a link to the OneConsultation admin portal and your demo public-facing virtual waiting room. You will then be able to test functionality and decide if you'd like to progress to a pilot phase. Everything after this point is optional. 

## Optional Step 5: Decide on users, room areas and customisations.

For trials, all users in your organisation are automatically granted access to use OneConsultation, and a single room area is created. However, there are a number of customisations you can make during the trial process, before you progress from trial to production, or at any time when in production. Please note all customisations can take up to 3 working days.

### Appearance
For both production and trial, it is possible to customise the appearance of the user-facing portal. The image, title text, explanatory wording and questions can all be changed. Provide us with details of any required changes.

### Virtual waiting rooms 
If you would like us to configure multiple virtual waiting room areas, you'll need to provide us with the details - we can give you a form for this.  

## Optional Step 6: check network firewall rules
Once in production it's likely that most users accessing OneConsultation will be doing so from outside of your corporate firewall, so no changes are necessary. Whilst conducting trials, however, you may be using OneConsultation within your corporate network boundary, in which case you should make sure that sufficient access is enabled to reach OneConsultation's video bridging services.

In order to use OneConsultation, ensure web-browser clients have access outbound to:

 - 51.140.26.197
 - 51.140.115.27
 - 13.94.141.192
 - 13.94.146.220
 - 40.71.84.17
 - 13.92.129.46
 
and to ensure that web-browser clients can use the following outbound ports in order to establish an audio/video call session:
 
 - TCP 33000–39999  (H.323 (Q.931/H.245 signaling)) 
 - TCP/UDP 40000–49999 (RTP/RTCP/RDP/DTLS/RTMP/STUN/TURN)
 
These are worldwide nodes to ensure that wherever users connect to the service from, they are routed to the most appropriate local node for the best audio & video experience.

## Optional Step 7: Define granular permission scopes
By default, everyone in your organisation will have access to all your OneConsultation rooms. If that's not appropriate, then you can specify more granular settings.

Access to a specific room can be restricted to a specific single Azure AD Security Group. This provides the flexibility to move users in and out of the Security Group without needing to reconfigure their access in OneConsultation. Access to a room includes the ability to see consultations, reports and recordings (where enabled).

To set up granular access, create or identify an Azure Active Directory Security Group. (not an on-premise AD group, or a Distribution/Office Group). Find the group in the [Azure Groups Management Blade](https://portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/AllGroups), and select it to view full details:

![Azure AD Management Blade](/images/azure-ad-groups.png)

Make a note of the *Object ID* and provide this information to us when we set up your new room (or to change an existing room setting). 

**Be sure to select a *Security Group* and not any other type of group.**

## Optional Step 8: Set up steps for recordings 
To enable consultation recordings, please see the additional [setup steps required here](recording_setup.md).
