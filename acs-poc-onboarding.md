# OneConsultation ACS Proof of Concept Onboarding Guide

## Introduction

Thank you for your help is validating this Proof of Concept (POC). The scope of this POC is to explore the use of an alternative media platform for OneConsultation consultations which will provide a more integrated experience with Microsoft Teams.

These steps can be performed alongside your existing OneConsultation rooms. You should ensure that any testing is done on non-production rooms and ensuring all parties know that testing of new technology is taking place. The usual standards of uptime and reliability may not nessecarily be applied to POC rooms.

## Prerequisite Steps

### Step 1: Re-consent to OneConsultation Permissions

Whilst logged in as a tenant admin, navigate to: https://login.microsoftonline.com/common/oauth2/authorize?resource=https://graph.windows.net&response_type=code&client_id=5637a6d7-9ce0-4788-b498-e96008b4ccb9&redirect_uri=https://admin.oneconsultation.net&scope=openid&prompt=admin_consent and review and accept the permissions reqested for the OneConsultation application. Note that there is an additional permission required in order to create online meetings:

Once you have accept these permissions you will be re-directed to the OneConsultation Admin Portal. Ensure you are still able to log in to the Admin Portal.

### Step 2: Nominate a service account for meeting creation

Consultations will be created as Microsoft Teams meetings, with the organiser of each meeting being the nominated service account. Create a new account or pick an existing account. Ensure this account has permission and license to create a Microsoft Teams meeting, and that the account will not become disabled due to policy (such as expiring password, MFA etc).

Identify and make note of this user's User (Object) ID in the [Azure user management portal](https://portal.azure.com/#blade/Microsoft_AAD_IAM/UsersManagementMenuBlade)

### Step 3: Create an Application Access Policy for OneConsultation

An Application Access Policy enables the OneConsultation application to act on behalf of the service user and create Microsoft Teams meetings.

Connect to Skype for Business PowerShell with an administrator account. For details, see [Manage Skype for Business Online with PowerShell.](https://docs.microsoft.com/en-us/microsoft-365/enterprise/manage-skype-for-business-online-with-microsoft-365-powershell)

Run the following cmdlets to create a new application access policy and assign it to the service user. In the second cmdlet, use the User (Object) ID of the service user:

```powershell
New-CsApplicationAccessPolicy -Identity OneConsultation-Meetings -AppIds "5637a6d7-9ce0-4788-b498-e96008b4ccb9" -Description "OneConsultation Meeting Creation Policy"
Grant-CsApplicationAccessPolicy -PolicyName OneConsultation-Meetings -Identity "SERVICE_USER_ID"
```

