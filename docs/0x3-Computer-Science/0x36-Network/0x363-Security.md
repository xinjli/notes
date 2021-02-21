# 0x363 Security

- [1. HTTP](#1-http)
    - [1.1. Authentication](#11-authentication)
        - [1.1.1. Basic Authentication](#111-basic-authentication)
        - [1.1.2. Sessions based authentication](#112-sessions-based-authentication)
        - [1.1.3. Token based Authentication](#113-token-based-authentication)
            - [1.1.3.1. JWT (Json Web Tokens)](#1131-jwt-json-web-tokens)
    - [1.2. Authorization](#12-authorization)
        - [1.2.1. OAuth](#121-oauth)
- [2. Reference](#2-reference)

## 1. HTTP
### 1.1. Authentication
First, we mention that Authentication and authorization are two different concepts
- authentication: verifying identify (401 Unauthorized)
- authorization: verifying permissions to a resource (403 Forbidden), 

In this section, we only summarize the authentication used in HTTP. There are 3 main authentication schemes used in HTTP.

- Basic authentication
- stateful (i.e. session using cookie)
- stateless (token using JWT/OAuth/...)

#### 1.1.1. Basic Authentication
It is using the Username/password scheme
It is Stateless authentication. every request will have to send both username and password . Defined in RFC7617

#### 1.1.2. Sessions based authentication
Session based authentication is a stateful method

**Flow**
The flow of session based authentication works as follows:

- user submit login credentials (e.g: email, password)
- server verifies the credential against the DB
- server create a temporary user session
- server issue a cookie with a session ID, the cookie will be stored on the client side and signed with a secret.
- user sends the cookie with each request
- server validates it against the session store & grants access
- when user logs out, server destroys the session and clears the cookie

**Features**
every user session is stored server-side (stateful). It can be saved in memory, cache or db.
each user is identified by a session ID (which is a random string), on the client side, it is stored in a cookie.
Horizontal scaling is more challenging using cookie

**Cookies**
cookie is a header (like Content-Type), it is set with Set-Cookie HTTP response by server, appended with Cookie by client
It consists of name, value (basically a map). typically will contain something like SESS_ID, but can contain other keys such as Domain
Domain and Path attributes can be used to specify a given site and route
Expiration can be used to expire cookie (when omitted, the cookie becomes a session cookie which will get deleted when browser is closed)
It also can have flags such as HttpOnly, Secure, SameSite

**Security**
signed with HMAC to migrate tampering
rarely encrypted (if ever, by AES) to protect from being read
HttpOnly (flag) cookies disable access from client side script, therefore migrate risk of XSS exploits


#### 1.1.3. Token based Authentication
Token-based authentication is a stateless method. 

**flow**
The typical token based authentication flow is as follows:

- user submits login credentials and server verifies those
- server generates a temporary token and embeds user data into it
- server responds back with the token
- user stores the token in client storage
- user sends the token along with each request
- server verifies the token and grant access
- when logout, token is cleared from client storage.

**Features**
- tokens are not stored server-side, only on the client side
- signed with a secret against tampering
- typically sent in Authentication header
- when is about to expire, it can be refreshed
- easily used in SPA web apps, web APIS, mobile apps

##### 1.1.3.1. JWT (Json Web Tokens)
JWT is an open standard for authentication and info exchange. 

It contains header (meta data), payload (claims) and signature (signed with symmetric or asymmetric key) delimited by dot

**Security** 
- signed with (HMAC)
- rarely encrypted (JWE)
- encoded (Base64Url) not for security but transport
- server need to maintain a blacklist of revoked tokens 
  
**Storage**

JWT can be stored in client storage, localStorage or SessionStorage
LocalStorage is domain-specific (5 MB per domain), plaintext, stored permanently

### 1.2. Authorization
#### 1.2.1. OAuth
OAuth is about access delegation, commonly used as a way for Internet users to grant websites or applications access to their information on other websites but without giving them the passwords, according to Wikipedia.

**Flow**
The rough flow of using OAuth is something like this:
- user (**resource owner**) first login into google (**resource server**) and another web service (**client**) - The web service wants to use some google's resource
- the web service sends a request to google's **authentication server** to ask permission to that resource
- google then ask the user whether the request is valid or not
- user verifies the request, then authentication server send a restricted token (JWT) to the service
- the service uses that restricted token to get resource from the **resource server**

Notice that resource server and authentication server are separated. The google's OAuth is [here](https://developers.google.com/drive/api/v3/about-auth)

## 2. Reference
Authentication on the web very good Youtube tutorial
