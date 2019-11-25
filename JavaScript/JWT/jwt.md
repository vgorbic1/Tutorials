## Jason Web Token (JWT)
JWT is an open standard defined by [RFC 7519](https://tools.ietf.org/html/rfc7519).
JWT is considered by its authors to be a **compact and self-contained way for securely 
transmitting information between parties as a JSON object**. JWT itself is composed of a Header, a 
Payload, and a Signature that proves the integrity of the message to the receiving server.

A JWT is an encoding format, and only an encoding format.

JWTs are loved because they are small, and lend themselves to efficient transport as part of a URL, 
as part of the POST parameter, or even within the HTTP header.
The JWT package contains everything the system would need to know about the user, and as such, 
can be delivered as a singular object.

A JWT is only secure when it’s used in tandem with encryption and transport security methodologies.
