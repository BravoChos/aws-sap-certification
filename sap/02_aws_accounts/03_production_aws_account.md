# Setting up the Production AWS Account

Follow the same steps to create a PRODUCTION AWS account as following.

- Create the AWS account named similar to your -GENERAL account but -PRODUCTION
- Add MFA to the account root user (and test it!!)
- Enable billing access for IAM users and set account contacts
- Add a billing ALARM to the PRODUCTION AWS Account.
- Add a BUDGET to PRODUCTION AWS Account (remember the checkboxes)


`Useful Notes!`

Remember the `gmail '+'` thick!! (very useful)! This will allow you to use the '+' sign in an email address. And this will mean that you can generate an infinite number of unique email addresses which all go back to the same Gmail account.

*Tip
Create as alias for your account!! (feat. IAM Dashboard)
## Adding an IAM Admin and user account

### Set user details 
    - User name
    - Select AWS access Types (Access key or password)
    
`IAM Access key`
Access keys are how the AWS Command Line Tools (CLI Tools) interact with AWS acc

- They are `Long-Term` Credentials

- An IAM User has 1 username and 1 password

- An IAM User can have two access keys (but never more!)

- Access keys can be `created`, `deleted`, made `inactive` or `active`

- AWS provides both Access keys ID and Secret Access keys whe you create Access key credentials.

- Once provided, there's no ablility to get access again (no future download)

- Make sure you keep the secrets access key safe and secure