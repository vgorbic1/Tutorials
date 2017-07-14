## Resource Modeling
A RESTful system is composed of resources. Resource is anything that has a URI.
You can Create, Update, Retrieve, or Delete a resource. These actions are mapped
to HTTP verbs POST, PUT, GET, and DELETE.

Resources are grouped in domains. A Domain is a cohesive set of resources.
To udentify proper domain and resource API Endpoints are used:
- Collection resource:
```
/room/reservation/v1
```
- Singleton resource:
```
/room/reservation/v1/{id}
```
Where **room** is a domain, **reservation** is resource, and **v1** is version.
