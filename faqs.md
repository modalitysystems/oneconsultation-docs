# Frequently Asked Questions 

_**What web browsers can I use OneConsultation with on my device?**_

You can find a list of supported browsers [here](browsers.md)

_**What's to stop uninvited guests joining my virtual consultation?**_ 

Each consultation takes place in a dynamically created meeting space created just for the purposes of that consultation, so there is no way for anyone else to join the consultation apart from the public user who created it, and any Office 365 users who have access to see it.

_**Is it possible to share my screen during a virtual consultation?**_ 

We're looking into ways that we can enable screen sharing for users joining OneConsultation with Microsoft Teams. See our [roadmap](roadmap.md) for details. A WebRTC version of OneConsultation is available that has screen sharing functionality built-in, and we can discuss this further with you case by case. 

_**Can OneConsultation record video calls?**_

Yes, this is now possible. All recordings are stored in your tenant, so there are some additional technical pre requisites and Azure Media Services cost implications. See our [recording setup](recording_setup.md) page for more details.

_**Where will the recordings be stored when this functionality is available?**_

Recordings will be stored in Azure Media Services in your tenant.

_**Are group virtual consultations possible through OneConsultation?**_

Yes, group consultations are possible with up to 20 total participants. We have two types of group consultation room available:
* Group session (all participants can see and hear each other)
* Auditorium (all particpants can hear each other, but only the host is visible) 
We can restrict access to these rooms via AD group, in the same way that we do for individual consultations. 

_**Can OneConsultation send invitations via SMS?**_

Yes, from the admin portal, an O365 user can send an SMS to a public user with a customisable message and a link to join a virtual consultation. The public user can simply click to join the video consultation straight away, which means they do not have to complete the pre-consultation questions to access the video call.
	
_**Is there extra cost associated with the SMS service?**_ 

Yes, depending on usage - this can be discussed with your Modality Systems account manager.  
	
_**Can OneConsultation send invitations via email?**_
 
No - OneConsultation is not intended to replace existing calendar management or appointment systems, and by design the product does not store any data or user information (like email addresses), so this functionality is not included on our roadmap.
  
_**Can third parties be added into a virtual consultation? For example, can a consultation take place with an O365 user, a public user, and a translator?**_

Yes, it's possible to add third parties into a virtual consultation using secure Internal and External join links.  
  
_**Can we customise the image on the public user login screen?**_

Yes, as long as the image is hosted somewhere by you, this can be whatever you like. 
  
_**Can we customise the image that a public user sees while they are waiting for their consultation to begin?**_

Not as standard - this is the default image for all users awaiting consultations. 
	
_**Can OneConsultation send a survey link after each consultation is finished?**_

Yes, this is possible using any web based survey like Microsoft Forms or SurveyMonkey. 
  
_**Can we have different post-consultation survey links for each different service/waiting room?**_

Yes, each 'service' (or waiting room) can have a different post-consultation survey link.
  
_**How is this product licenced?**_

There are no licence keys for OneConsultation. The product is licenced on a concurrent connection basis - that is, how many users are connected into virtual consultations at any one time.
	
_**What is a concurrent connection?**_

A concurrent connection is 1(one) user who is connected to a video consultation. So an in-progress consultation with one public user and one O365 user makes up 2(two) concurrent connections.
	
_**How do I know how many concurrent connections I need?**_

This will vary depending on the size and scale of your organisation and how much you'd like to use the video consultation service. Our team of experts can guide you to an appropriate estimate.
  
_**What data does OneConsultation store?**_

The system does not store any user data at rest. Public user information gathered via the pre-consultation questions is only stored in memory for the purposes of displaying in the Admin Portal, and is never persisted to an at rest service. 
	
_**Where is OneConsultation hosted?**_

OneConsultation is hosted in Microsoft Azure and therefore adheres to Microsoft security practices for access to any part of the service.
	
_**What if my organisation isn't using Microsoft Teams or Skype for Business? Can I still use OneConsultation?**_

Yes, we have a WebRTC solution to this that our Account Managers can discuss with you. 

_**What else is on the product roadmap?**_

See our full [roadmap](roadmap.md) for details.

_**Is there a recommended broadband speed for OneConsultation?**_

Ofcom and the UK goverment recommend that a 'decent' broadband speed is for typical home usage is one capable of delivering a download speed of at least 10 Mbps and an upload speed of at least 1 Mbps. You can find more information on this in the [House of Commons library](https://commonslibrary.parliament.uk/constituency-casework/broadband-faqs/) and  advice on your rights around broadband on [Ofcom's website](https://www.ofcom.org.uk/phones-telecoms-and-internet/advice-for-consumers/broadband-uso-need-to-know)

_**If I'm using 4G to connect to OneConsultation, how much mobile data would a consultation typically use?**_

We estimate that a 30 minute consultation would use approximately 126mb of data. 
