## Authorization

In most standard implementations, including those featured by ASP.NET, the authorization phase 
kicks in right after the authentication, and it’s mostly based on permissions or roles: any 
authenticated user might have their own set of permissions and/or belong to one or more roles, 
and thus be granted access to a specific set of resources. These role-based checks are usually 
set by the developer in a declarative fashion within the application source code and/or 
configuration files.

Authorization, like we said, shouldn’t be confused with [authentication](https://github.com/vgorbic1/Tutorials/blob/master/Security/authentication.md), despite the fact it could 
be easily exploited to perform an implicit authentication as well, especially when it’s delegated 
to a third-party actor.

### Third-party Authorization
The best known third-party authorization protocol nowadays is the 2.0 release of OAuth, also 
known as **OAuth2**, which supersedes the former release (OAuth1 or simply OAuth) originally 
developed by Blaine Cook and Chris Messina in 2006.

We already talked a lot about it for good reasons: OAuth 2 has quickly become the 
industry-standard protocol for authorization and is currently used by a gigantic amount of 
community-based websites and social networks, including Google, Facebook and Twitter. 
It basically works like this:
1. Whenever an existing user requests a set of permissions to our application via OAuth, 
we open a transparent connection interface between them and a third-party authorization 
provider that is trusted by our application (for example, Facebook).
2. The provider acknowledges the user and, if they have the proper rights, responds 
entrusting them with a temporary, specific access key.
3. The user presents the access key to our application and will be granted access.

We can clearly see how easy it is to exploit this authorization logic for authentication purposes as 
well; after all, if Facebook says I can do something, shouldn’t it also imply that I am who I claim 
to be? Isn’t that enough?

The short answer is no. It might be the case for Facebook, because their **OAuth 2** implementation 
implies that the subscriber receiving the authorization must have authenticated himself to 
Facebook first; however, this assurance is not written anywhere: considering how many websites 
are using it for authentication purposes we can assume that Facebook won’t likely change their 
actual behaviour, yet we have no guarantees about it.

