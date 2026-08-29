 - Subscriptions are a unit of management, billing, and scale. Controls billing separate from access.
 - Two types of subscription boundaries: billing and access control boundaries.
 - Management groups sit above subscriptions.
 - Every Microsoft Entra tenant has a single top-level Tenant Root Group.
 - Nexting can support up to 6 levels deep (excluding the root and subscription levels)
 - 10,000 management groups
  
- Entra ID
  - Entra Connect syncs user identities between on-prem AD and Entra ID (Azure cloud). Bi-directional sync.
  - Entra Domain Services. Managed domain services - domain join, group policy, LDAp, and Kerberos/NTLM authentication without you deploying domain controllers in the cloud. Useful for legacy applications that can't use modern auth.
    - Domain Services integrated with existing Entra tenant so users cn sign into the managed domain with their existing Entra credentials.
    - Existing groups and user accounts also carry over, providing a smoother migration path.
    - This is a separate, fully managed DS; it is not an extension of your existing on-prem AD.
    - one-way sync from Entra ID to Entra DS. (does not sync back to Entra ID)
- Authentication methods:
 1) Password only
 2) MFA (something you have + something you know)
 3) Passwordless (something you have + something you know/are)
  
- Single Sign-On (SSO) - sign in once and access multiple trusted applications. SSO reduces password sprawl.
- Multifactor Authentication (MFA)
 1) something the user knows (password or challenge question)
 2) something the user has (a code sent to mobile phone)
 3) something the user is (a biometric signal such as fingerprint or face scan)
- Passwordless (replaces traditional password with a trusted device plus a biometric signal or pin). Entra ID supports 3 passwordless options
 1) Windows Hello for Business (biometric or PIN)
 2) Microsoft Authenticator App (mobile app uses biometric/PIN + number match)
 3) FIDO2 security keys (external hardware device with hardware cryptographic key)
  
  
- Entra External ID includes capabilities used to securely interact with external identities (person, device, or service that exists outside of your tenant).
  The external identity provider manages authentication and you manage authorization to your apps with Entra ID or Azure AD B2C.
- External ID Capabilities:
 1) B2B Collaboration - invitation sent or self-service. External ID manages authorization. Guest users appear in your directory as guest user objects.
 2) B2B Direct Connect - mutual 2-way trust to another Entra tenant. Good for sharing Teams Shared Channels only.
 3) External Id for Customers (formerly Azure AD B2C) - users sign up or sign in with your published apps (excluding Microsoft apps). Users are managed in a separate External ID tenant.
  
- Azure Conditional Access is a tool Microsoft users to allow or deny access to resources based on identity signals. (Signal -> Decision -> Enforcement)
  
- Zero Trust Model - Assumes worst case scenario; assumes breach at the outset and then verifies each request.
 1) Verify explicitly
 2) Use least privilege access
 3) Assume Breach - limit the potential impact and segment access. Verify end-to-end encryption.
   
- Defense in Depth - layered security
 1) Physical Security - protect datacenter hardware
 2) Identity and Access - secure identities, grant least access
 3) Perimeter - protect against network based attacks
 4) Network - segment and restrict communication
 5) Compute - patch systems, protect endpoints
 6) Application - eliminate vulnerabilities in code
 7) Data - protect confidentialityk, integrity, availability
  
- Azure Key Vault protects:
 1) Secrets (connection strings, passwords, API keys)
 2) Encryption Keys
 3) Certificates (TLS/SSL certificates, auto-renewal, lifecycle management)
  
  
