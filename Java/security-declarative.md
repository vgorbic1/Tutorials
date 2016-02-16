## Declarative Security
Two major aspects to securing Web applications:
- Preventing unauthorized users from accessing sensitive data. This process involves access restriction (identifying which resources
need protection and who should have access to them) and authentication (identifying users to determine if they are one of the authorized
ones).
- Preventing attackers from stealing network data while it is in transit. This process involves the use of Secure Sockets Layer (SSL)
to encrypt the traffic between the browser and the server.

**Declarative security** means that none of the individual servlets or JSP pages need any security-aware code. Instead, both of the major security aspects are handled
by the server.

To prevent unauthorized access, you use the Web application deployment descriptor (web.xml) to declare that certain URLs need protection.
You also designate the authentication method that the server should use to identify users. At request time, the server automatically
prompts users for usernames and passwords when they try to access restricted resources, automatically checks the results against a predefined
set of usernames and passwords, and automatically keeps track of which users have previously been authenticated. This process is completely 
transparent to the servlets and JSP pages.
