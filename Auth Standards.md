---
tags:
  - zettelkasten
topic:
  - auth
createAt: 2024-03-31 15:25
---
# OAuth2 - since 2013 (Oauth was 2006)
it's an industry standard where an application is asking for data from other applications. imagine that we build our application, and then we want to build an OAuth2 application asking for some data from Facebook. So we'll need to build communication between our apps and Facebook. In our application, we can ask the user to go to Facebook and authorize our application to read the data given by Facebook after the user allows it.
# OIDC (OpenID Connect) - since 2014
it's built on top of the OAuth2 standard. Now after you realize that we can get the data from the OpenID Provider, we can use that data to identify the user and allow it as authentication.
# SAML (Security Assertion Markup Language) - since 2002
It's more enforcing than OIDC since it only allows one specific External Identity Provider and uses XML (older standard). The flow is pretty similar with just a bit older standard. 
# Radius (Remote Authentication Dial-In User Service) - since 1991
an older standard that's commonly used for network access (for WIFI)
# LDAP - since 1980s
It's standard to store the user list. usually, it's a central database system to store users. can expose it's data via OIDC or SAML

see also:
- [[Auth Provider Options]]