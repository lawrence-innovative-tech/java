#### **Purpose
- keycloak controls centralised authentication and authorization, Developed by red hat handover to CNCF.
- Keycloak supports IdP(identity providers) and centralised user-management system like our env.
- Keycloak uses SSO(Single Sign On/Out) mechanism. A user login once and access all the application if user has permission.
- Keycloak helps to achieve Restful api rules for stateless access via Jwt tokens issued by keycloak.
- Keycloak to achieve RBAC (Role Based Access Control).
#### **Realm
- Realm is logical container it holds user, clients, roles, user-management are isolated from others.

#### **User / Client / Group
- Client is application or Service accounts
- Group - group to categories users. 
#### **Roles
- This roles define the user permissions, Two to to assign roles,
	1. Direct user to Assign roles.
	2. Assign group -> group has user.
	3. Subgroup under group both access point have that particular user.
#### **OIDC (OpenID Connect)
- It wraps OAuth 2.0 + user details.
- It modern way to authorization, it hold user details to user permission (OAuth 2.0).
- SAML uses heavy xml, but it holds jwt with json easy to carry.
#### **OAuth 2.0
- It maintain only authorization alone.
- Fully redesigned for token based authorization, instead of older version 1.0 signature based. 
