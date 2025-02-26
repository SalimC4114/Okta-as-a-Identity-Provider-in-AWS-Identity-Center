# Okta-as-a-Identity-Provider-in-AWS-Identity-Center
In this project, I integrated Okta as an Identity Provider (IdP) for AWS Identity Center (formerly AWS SSO). This setup allows users to log into AWS using their Okta credentials, making access management much more secure and streamlined.

Overview
In this project, I integrated Okta as an Identity Provider (IdP) for AWS Identity Center (formerly AWS SSO). This setup allows users to log into AWS using their Okta credentials, making access management much more secure and streamlined.  Now, with Okta handling authentication, users sign in once and get secure access to AWS based on their assigned roles. 
What I Did
Configured Okta as an external IdP using SAML 2.0
Linked Okta user groups to AWS IAM roles for role-based access
Uploaded metadata between Okta and AWS to establish the trust connection
Tested Single Sign-On (SSO) to ensure seamless login from Okta to AWS
Tech & Skills Used
Okta Developer Account – Configured SAML 2.0, set up user/group mappings
AWS Identity Center – Enabled SSO, mapped roles in IAM
Identity & Access Management (IAM) – Secured AWS access with role-based permissions
Step 1: Enable AWS Identity Center
Log into the AWS Management Console.
Navigate to AWS Identity Center (Search for it in the AWS Console).
If not already enabled, click Enable AWS Identity Center.
In the left panel, go to Settings > Identity Source.
Click Change identity source → Select External Identity Provider → Click Next.
Select SAML 2.0-based authentication.
Click Download metadata file (you'll upload this to Okta later).
Step 2: Configure Okta as an Identity Provider for AWS
Log into Okta Admin Console.
Navigate to Applications > Applications.
Click Create App Integration → Select SAML 2.0 → Click Next.
App Name: Enter AWS Identity Center → Click Next.

Step 3: Configure SAML Settings
Under Sign-on go to Settings, locate:
Single sign-on URL → Use the AWS ACS URL from the metadata file.
Audience URI (SP Entity ID) → Use the AWS SAML Entity ID from the metadata file
Under SAML Signing Certificates > actions > view metadata and copy the entity id and the end point location.
In AWS, add the end point under IdP sign-in URL and entity id with the issuer URL. Also add the okta cert file. (Actions > download cert)
Accept and confirm.
Step 4: Provisioning 
Scroll to Provisioning, then click Enable automatic provisioning
Copy the SCIM endpoint URL and Access Token (you'll need this for Okta)
In Okta, Click Provisioning > Configure API Integration
Check Enable API Integration
Paste the SCIM endpoint URL from AWS
Enter the Access Token from AWS
Click Test API Credentials → It should confirm the connection
Click Save
Under To App, click Edit
Enable Create Users, Update User Attributes, and Deactivate Users
Click Save
Step 5: Assign Users & Groups in Okta
Go to Assignments in the AWS Identity Center app in Okta
Click Assign > Assign to People or Groups
Choose the users or groups you want to provision to AWS
Click Save and Done
Now, Okta will automatically sync users and groups to AWS Identity Center via SCIM! 
Step 6: Test the Setup
Create a new user in Okta and assign them to the AWS Identity Center app
Wait a few minutes for SCIM to sync (or force a sync in Okta)
Check AWS Identity Center > Users to confirm the new user appears
 Remove a user from the Okta group and confirm it deactivates in AWS
Next Steps
Want to enhance this? You can:
Enable Just-in-Time (JIT) provisioning for faster user access
Use Okta Workflows to automate user lifecycle management
Integrate MFA policies for extra security
