# Table of Content

1. **[Web](#1-web)**
   * **[1.1 OAuth2](#11-oauth2)**
   * **[1.2 OpenId Connect](#12-openid-connect)**
   * **[1.3 Fido2](#13-fido2)**
2. **[Cloud](#2-cloud)**
3. **[Android](#3-android)**
4. **[Util](#4-util)**

# 1. Web

### 1.1 OAuth2

- protocol to authorize api requests
- token represents authorization of application to act on users behalf

#### 1.1.1 Roles

**Resource Owner:** owner of (some of the) resources on a resource server<br><br>
**Resource Server:** stores protected resources. Allows access to resources based on access tokens<br><br>
**Client:** application that wants to access resources of resource owner on resource server<br><br>
**Authorization Server:** provides access tokens for resources on resource server, for a access scope defined by the resource owner

#### 1.1.2 Authorization Grant Types/Flows

**Authorization Code:**<br>
&#8594; client app redirects user to authorization service together with client id<br>
&#8594; user logs in and authorizes client app<br>
&#8594; auth service redirects including auth code<br>
&#8594; client app requests access token using auth token and client secret<br>
- What is the purpose of the access token, when we just could use the auth token?<br>
&#8594; Auth token is transmitted through frontend (front channel) and could be stolen<br>
&#8594; Access token can only be requested with auth token together with client secret (using back channel)<br>
&#8594; Implicit flow can be used for front channel only apps (requests access token directly)<br>

**Authorization Code with PKCE (Proof Key for Code Exchange):**<br>
&#8594; Instead of using client_secret it uses a temporary value<br>
&#8594; Client generates a random number (code_verifier) and hashes this number (code_challenge)<br>
&#8594; Client sends the hash and the hash-method (code_challange_method) to auth server with redirect to get auth-code<br>
&#8594; Auth Server sends back auth code<br>
&#8594; To get access token (instead of sending client secret), the client sends the code_verifier<br>
- Useful for front channel only apps<br>

**Client Credentials:**<br>
&#8594; app sends its client credentials (clientId and clientSecret) to auth server<br>
&#8594; auth server returns access token<br>
- used to access client apps own account<br>

**Client Credentials:**<br>
&#8594; client app sends request to device authorization endpoint of auth service<br>
&#8594; auth service returns url to authorize<br>
&#8594; client app presents url to user<br>
&#8594; client app polls access endpoint<br>
&#8594; user uses url to login and authorize client app<br>
&#8594; client app gets auth token from access endpoint<br>

### 1.2 OpenId Connect

- authentication protocol based on top of OAuth2
- standardizes authentication with OAuth2
- openid scope is added to request to auth server
- adds user info endpoint to authorization server
- additionally, to auth token, auth server returns id token
  &#8594; id token can be directly used by client to identify user

### 1.3 Fido2

# 2. Cloud

**Virtualization:**
Abstraction of hardware or software<br>
&#8594; Multiple ssd storages could be pooled as one storage location<br>
&#8594; Multiple servers could virtualize one powerful server<br>
&#8594; cloud service can abstract away a software installation like S3 for Hadoop

# 3. Android

### 3.1 OAuth2

- Available Accounts can be retrieved via AccountManager
- Token can be retrieved via AccountManager &#8594; AccountManager uses service provided by account owner app (i.e Microsoft, Google, etc) to get auth token
- AccountManager caches token until AccountManager.invalidateAuthToken() is invoked

# 4. Util

- check wsl2 status: wsl --list --verbose

