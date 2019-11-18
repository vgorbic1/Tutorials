## Web Feature Service

Web Feature Service (WFS) is an Interface Standard. It llowing requests for geographical features 
("source code" behind a map) across the web using platform-independent calls.

Web Map Service (WMS) interface (or online tiled mapping portals like Google Maps) returns only an image, 
which end-users cannot edit or spatially analyze. 

The XML-based Geography Markup Language (GML) furnishes the default payload-encoding for transporting 
geographic features, but other formats like shapefiles can also serve for transport.

The OGC (Open Geospatial Consortium) membership defined and maintains the WFS specification.

When writing a WFS, you must implement the following operations:
- GetCapabilities - this queries the WFS service to determine available options.
- DescribeFeatureType - this retrieves the XML schema to allow the WFS client to parse the resultsets.
- GetFeature - this performs the actual query - parameters such as bounding box and any other filters should 
be passed in, as appropriate, and the WFS service then returns a GML resultset containing full geometry 
and feature attributes.

It is rare to find a WFS hosting features you need, if your needs are very specific. The reason why Web Feature 
Services are relatively rare is because of the large amounts of data that must be transmitted to describe a whole 
feature. It is therefore not very cost-effective to host a WFS rather than a WMS, which sends only images.

The most common type of WFS you’ll encounter will therefore probably be on a local network or even on your own 
computer, rather than on the Internet.

### REST or RPC
Representational State Transfer (REST) is all about a client-server relationship, where server-side data 
are made available through representations of data in simple formats, often JSON and XML.

Hypermedia is fundamental to REST, and is essentially just the concept of providing links to other resources.

Before REST became popular (after companies such as Twitter and Facebook labeled their APIs as REST), most 
APIs were built using an XML-RPC or SOAP. In XML, a lot of things are just strings, so you need to layer 
meta data on top in order to describe things such as which fields correspond to which data types. 
The **RPC** part stands for “remote procedure call,” and it’s essentially the same as calling a function 
in JavaScript, PHP, Python and so on, taking a method name and arguments.

RPC is just a bunch of functions, but in the context of an HTTP API, that entails putting the method in 
the URL and the arguments in the query string or body. 

- RPC-based APIs are great for actions (that is, procedures or commands).
- REST-based APIs are great for modeling your domain (that is, resources or entities), making CRUD 
(create, read, update, delete as GET, POST, PUT, DELETE, OPTIONS and, hopefully, PATCH) available for all of 
your data. RPC, however, would not do that. Most use only GET and POST, with GET being used to fetch 
information and POST being used for everything else.

#### Example: 
It is common to see RPC APIs using something like 
```
POST /deleteFoo, with a body of { “id”: 1 }
```
 instead of the REST approach, which would be 
```
DELETE /foos/1
```

- If an API is mostly actions, maybe it should be RPC.
- If an API is mostly CRUD and is manipulating related data, maybe it should be REST.

[SOURCE](https://www.smashingmagazine.com/2016/09/understanding-rest-and-rpc-for-http-apis/)
