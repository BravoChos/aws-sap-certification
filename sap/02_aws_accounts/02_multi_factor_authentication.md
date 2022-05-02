# AWS Multi-Factor Authentication

<img src="./asset/mfa_diagram.png" width="90%">

<br/>

AWS Multi-Factor Authentication (MFA) is a simple best practice that adds an extra layer of protection on top of your user name and password. With MFA enabled, when a user signs in to an AWS Management Console, they will be prompted for their user name and password (the first factor—what they know), as well as for an authentication code from their AWS MFA device (the second factor—what they have). Taken together, these multiple factors provide increased security for your AWS account settings and resources.

<br/>

<img src="./asset/mfa.png" width="60%">

<br /> 

Without MFA, a static user name and an infrequently changing password are needed to login. This is known as one factor.

Adding a second factor, something only user has, makes it more secure. The MFA device/app generates a code which changes every 30s.  This code is needed together with user's username and password.

## MFA/OTP Applications (Google it!)
- iOS Google Authenticator
- Android Google Authenticator
- 1Password: https://1password.com
- Authy : https://authy.com/