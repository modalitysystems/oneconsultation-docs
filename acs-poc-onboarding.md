# OneConsultation ACS Proof of Concept Onboarding Guide

## Introduction

Thank you for your help is validating this Proof of Concept (POC). The scope of this POC is to explore the use of an alternative media platform for OneConsultation consultations which will provide a more integrated experience with Microsoft Teams.

These steps can be performed alongside your existing OneConsultation rooms. You should ensure that any testing is done on non-production rooms and ensuring all parties know that testing of new technology is taking place. The usual standards of uptime and reliability may not nessecarily be applied to POC rooms.

# Prerequisite Steps

## Step 1: Enable federation for ACS Resources

Please complete the [ACS Resource Enablement form](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR21ouQM6BHtHiripswZoZsdURDQ5SUNQTElKR0VZU0VUU1hMOTBBMVhESS4u) to request enablement of your tenant. You can continue with the other steps whilst this request is being processed.

## Step 2: Re-consent to OneConsultation Permissions

Whilst logged in as a tenant admin, navigate to: [https://login.microsoftonline.com/common/oauth2/authorize?resource=https://graph.windows.net&response_type=code&client_id=5637a6d7-9ce0-4788-b498-e96008b4ccb9&redirect_uri=https://admin.oneconsultation.net&scope=openid&prompt=admin_consent](https://login.microsoftonline.com/common/oauth2/authorize?resource=https://graph.windows.net&response_type=code&client_id=5637a6d7-9ce0-4788-b498-e96008b4ccb9&redirect_uri=https://admin.oneconsultation.net&scope=openid&prompt=admin_consent). Review and accept the permissions reqested for the OneConsultation application. Note that there is an additional permission required in order to create online meetings:

![OneConsultation Permissions](https://raw.githubusercontent.com/modalitysystems/oneconsultation-docs/master/images/2021-02-11%2013_11_19-Window.png "OneConsultation Permission Request")

Once you have accept these permissions you will be re-directed to the OneConsultation Admin Portal. Ensure you are still able to log in to the Admin Portal.

## Step 3: Nominate a service account for meeting creation

Consultations will be created as Microsoft Teams meetings, with the organiser of each meeting being the nominated service account. Create a new account or pick an existing account. Ensure this account has permission and license to create a Microsoft Teams meeting, and that the account will not become disabled due to policy (such as expiring password, MFA etc).

Identify and make note of this user's User (Object) ID in the [Azure user management portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UsersManagementMenuBlade)

### Will the service account show up anywhere?

The service account is used to create the Microsoft Teams meetings used for consultations. The service account is NOT added to any meetings, but as the meeting owner is shown by default in the "Others from chat" section as an invitation suggestion. Bear this in mind when choosing a name for the service account.

![Service Account Name shown in Teams meeting](https://raw.githubusercontent.com/modalitysystems/oneconsultation-docs/master/images/2021-02-11%2014_54_40-ONECONSULTATION21de90fa-a517-4e8d-a5be-72845603a058%20_%20Microsoft%20Teams.png "Service account name shown in Teams meeting")

## Step 4: Create an Application Access Policy for OneConsultation

An Application Access Policy enables the OneConsultation application to act on behalf of the service user and create Microsoft Teams meetings.

Connect to Skype for Business PowerShell with an administrator account. For details, see [Manage Skype for Business Online with PowerShell.](https://docs.microsoft.com/en-us/microsoft-365/enterprise/manage-skype-for-business-online-with-microsoft-365-powershell)

Run the following cmdlets to create a new application access policy and assign it to the service user. In the second cmdlet, use the User (Object) ID of the service user:

```powershell
New-CsApplicationAccessPolicy -Identity OneConsultation-Meetings -AppIds "5637a6d7-9ce0-4788-b498-e96008b4ccb9" -Description "OneConsultation Meeting Creation Policy"
Grant-CsApplicationAccessPolicy -PolicyName OneConsultation-Meetings -Identity "SERVICE_USER_ID"
```

> If the service user is newly created, it can take up to 24 hours before the User ID is recognised by the Grant-CsApplicationAccessPolicy cmdlet.

Once these steps have been completed, provide the User (Object) ID when requested in order to complete your setup.



