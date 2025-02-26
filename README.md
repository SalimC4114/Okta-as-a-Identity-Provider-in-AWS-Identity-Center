# Okta-as-a-Identity-Provider-in-AWS-Identity-Center
In this project, I integrated Okta as an Identity Provider (IdP) for AWS Identity Center (formerly AWS SSO). This setup allows users to log into AWS using their Okta credentials, making access management much more secure and streamlined.

## Overview
In this project, I integrated **Okta as an Identity Provider (IdP) for AWS Identity Center** (formerly AWS SSO). This setup allows users to log into AWS using their Okta credentials, making access management much more secure and streamlined. Now, with Okta handling authentication, users sign in once and get secure access to AWS based on their assigned roles.  

## What I Did
- Configured **Okta as an external IdP** using **SAML 2.0**  
- Linked **Okta user groups to AWS IAM roles** for role-based access  
- Uploaded metadata between Okta and AWS to establish the trust connection  
- Tested **Single Sign-On (SSO)** to ensure seamless login from Okta to AWS  

## Tech & Skills Used
- **Okta Developer Account** – Configured **SAML 2.0**, set up user/group mappings  
- **AWS Identity Center** – Enabled **SSO**, mapped roles in **IAM**  
- **Identity & Access Management (IAM)** – Secured AWS access with **role-based permissions**  

---

## Step 1: Enable AWS Identity Center
1. Log into the **AWS Management Console**.
2. Navigate to **AWS Identity Center** (Search for it in the AWS Console).
3. If not already enabled, click **Enable AWS Identity Center**.
4. In the left panel, go to **Settings > Identity Source**.
5. Click **Change identity source** → Select **External Identity Provider** → Click **Next**.
6. Select **SAML 2.0-based authentication**.
7. Click **Download metadata file** (you'll upload this to Okta later).

---

## Step 2: Configure Okta as an Identity Provider for AWS
1. Log into **Okta Admin Console**.
2. Navigate to **Applications > Applications**.
3. Click **Create App Integration** → Select **SAML 2.0** → Click **Next**.
4. **App Name:** Enter **AWS Identity Center** → Click **Next**.

---

## Step 3: Configure SAML Settings
1. Under **Sign-on**, go to **Settings**, locate:
   - **Single sign-on URL** → Use the **AWS ACS URL** from the metadata file.
   - **Audience URI (SP Entity ID)** → Use the **AWS SAML Entity ID** from the metadata file.
2. Under **SAML Signing Certificates**:
   - Click **Actions > View Metadata**, copy the **Entity ID** and **Endpoint Location**.
3. In **AWS**, add the **Endpoint Location** under **IdP sign-in URL** and **Entity ID** under **Issuer URL**.
4. Upload the **Okta certificate file** to AWS (**Actions > Download Cert** in Okta).
5. Accept and **Confirm**.

---

## Step 4: Enable User Provisioning (SCIM) in AWS & Okta
1. In **AWS Identity Center**, go to **Settings > Identity Source**.
2. Scroll to **Provisioning**, then click **Enable automatic provisioning**.
3. Copy the **SCIM endpoint URL** and **Access Token** (you'll need this for Okta).
4. In **Okta**, navigate to **Provisioning > Configure API Integration**.
5. Check **Enable API Integration**.
6. Paste the **SCIM endpoint URL** from AWS.
7. Enter the **Access Token** from AWS.
8. Click **Test API Credentials** → It should confirm the connection.
9. Click **Save**.
10. Under **To App**, click **Edit**.
11. Enable:
    - **Create Users**
    - **Update User Attributes**
    - **Deactivate Users**
12. Click **Save**.

---

## Step 5: Assign Users & Groups in Okta
1. Go to **Assignments** in the AWS Identity Center app in Okta.
2. Click **Assign > Assign to People or Groups**.
3. Choose the users or groups you want to provision to AWS.
4. Click **Save and Done**.

Now, Okta will automatically sync users and groups to AWS Identity Center via **SCIM**! 🚀

---

## Step 6: Test the Setup
1. **Create a new user** in Okta and assign them to the **AWS Identity Center app**.
2. Wait a few minutes for **SCIM to sync** (or force a sync in Okta).
3. Check **AWS Identity Center > Users** to confirm the new user appears.
4. **Remove a user** from the Okta group and confirm it **deactivates in AWS**.

---

## Next Steps
Want to enhance this? You can:
- 🔹 Enable **Just-in-Time (JIT) provisioning** for faster user access.
- 🔹 Use **Okta Workflows** to automate user lifecycle management.
- 🔹 Integrate **MFA policies** for extra security.

This setup ensures **secure, automated user provisioning** and **seamless access management** between Okta and AWS Identity Center!
