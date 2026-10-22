Today i learnt about Microsoft Entra ID Governance

It solves the issues relating to user management in an organisation, automating an identity lifecycle, within a cloud environment, a close similarity is OKTA which helps manage either cloud or on-premise authentication and authorization.

Microsoft Entra ID Governance unlike OKTA which is cloud agnostic id built on the microsoft ecosysystem, mannages online and on-premises access for user in an organisation.

It makes use of lifecycle workflows managing a user lifecycle within three phases.
Joiner, Mover, Leaver.

Joiner : Using our organisational unit structure from the readme, say we have John join as a software Engineer, John automaticcaly is configured with access that allows to read, create, and edit files in the Engineering Project Share.

Mover: Over time John moves to a Security operation role, using Microsoft Entra Id to manage governance, John no longer has access to create and edit files, but is limited to read, in the Engineering Project Share, which is enough for the security role which includes but not limited to Monitoring and keeping logs

Leaver: When John leaves NDIA, IT disables his AD account, removes his resource-access group memberships including any remaining Engineering read access and Security Operations access and moves the disabled account into the DisabledUsers OU.

WHEN TO USE LIFECYCLE FLOWS

- Automating and extendinguser orientation and HR provisioning
- workflow history and auditing
- integrating with Logic apps
