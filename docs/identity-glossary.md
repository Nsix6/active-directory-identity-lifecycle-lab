# active-directory-identity-lifecycle-lab

1. Authentication:
   In simple words refers to verifying an identity, an identity could be a person, software, or machines which requires access to protected assests. Most times this is done using attribute that represents a person or software, example inclues email addresses, sign-in credentials(username/password), a government issued ID, a MAC address e.t.c

2. Authorization:
   This follows quite after authentication, now we are able to verify an identity, this goes a step further, this determines what exactly the verified identity has access to do, think about this as the scope, ensuring identities even while verified do not have broad access without control.

3. Directory:
   A centralized system that stores and organizes information about identities and resources, allowing administrators and applications to find and manage them.
   At our fictional company, Active Directory stores employee accounts, computer accounts, and security groups. IT administrators use it to manage employee identities and access.

4. Service Provider (SP):
   A Service Provider is an application or service that relies on an Identity Provider (IdP) to authenticate users.
   - Identity Provider (IdP): Checks who you are.
     Service Provider (SP): Provides the application you want to use after your identity is verified.

5. Role-Based Access Control (RBAC):
   This defines permission given to an entity based on the roles assigned , it includes a scope which helps limit actions/permissions for the entity involved. An entity could be a group, user, or a service.

6. Attribute-Based Access Control (ABAC):
   Unlike the RBAC, this provides permissions/authorization based on attributes, using tags that both the service providers and the entity needing access needs to have. one main advantage is it alows for dynamic access over the rigidity of roles RBAC.
7. Least Priviledge:
   An identity should receive only the permissions necessary to perform its assigned responsibilities, not unrestricted administrative access.
