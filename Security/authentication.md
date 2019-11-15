## Authentication

Since the origin of the World Wide Web, the vast majority of authentication 
techniques rely upon HTTP/HTTPS implementation standards, and all of them work
more or less in the following way:
1. A non-authenticated user-agent asks for a content that cannot be accessed without 
some kind of permissions.
2. The web application returns an authentication request, usually in form of an HTML 
page containing an empty web form to complete.
3. The user-agent fills up the web form with their credentials, usually a username and 
a password, and then sends it back with a POST command, which is most likely issued 
by a click on a Submit button.
4. The web application receives the POST data and calls the aforementioned server-side 
implementation that will try to authenticate the user with the given input and return
an appropriate result.
5. If the result is successful, the web application will authenticate the user and store 
the relevant data somewhere, depending on the chosen authentication method: sessions/cookies, 
tokens, signatures, and so on. Conversely, the result will be presented to the user as a 
readable outcome inside an error page, possibly asking them to try again, contact an 
administrator, or something else.

### Third-party authentication
Being forced to have a potentially different username and password for each website visit can 
be frustrating, other than requiring the users to develop custom password storage techniques 
that might lead to security risks. In order to overcome this issue a wide amount of IT 
developers started to look around for an alternative way to authenticate users that could 
replace the standard authentication technique based upon usernames & passwords with an authentication 
protocol based upon trusted third-party providers.

The first successful attempt to do that was the first release of **OpenID**, an open and decentralized 
authentication protocol promoted by the non-profit OpenID Foundation. Available since 2005, it was 
quickly and enthusiastically adopted by some big players such as Google and StackOverflow,
who originally based their authentication providers upon it. Here’s how it worked in few words:
1. Whenever our application receives an OpenID authentication request, it opens a transparent 
connection interface through the requesting user and a trusted, third-party authentication provider 
(for example, the Google Identity Provider): the interface can be a popup, an AJAX, 
populated modal windows or an API call, depending on the implementation.
2. The user sends his username and password to the aforementioned third-party provider, who performs 
the authentication accordingly and communicates the result to our application by redirecting the user 
back to where he came, together with a security token that can be used to retrieve the authentication 
result.
3. Our application consumes the token to check the authentication result, authenticating the user 
in case of success or sending an error response in case of failure.

In a desperate attempt to keep their flag alive after the takeover of the OAuth/OAuth2 social logins, 
the OpenID foundation released in february 2014 the “third generation” of the OpenID technology, which 
was called **OpenID Connect**.

The choice to move to OpenID Connect was quite sad in 2014 and it still is as of today: however, 
after more than three years, we can definitely say that – despite its undeniable limitations – 
OpenID Connect can still provide a useful, standardized way to obtain user identity; it allows 
developers to request and receive info about authenticated users and sessions using a 
convenient, RESTful based JSON interface; it features an extensible specification wich also 
supports some promising optional features such as encryption of identity data, auto-discovery of 
OpenID providers, and even session management. In short, it’s still useful enough to be used instead 
of relying to pure OAuth2.

[OpenID Connect](http://openid.net/specs/openid-connect-core-1_0.html)

[SOURCE](https://www.ryadel.com/en/user-authentication-authorization-web-development-login-auth-identity/)
