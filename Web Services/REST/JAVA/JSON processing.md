## Processing JSON Data

By the term processing, we
mean reading, writing, querying, and modifying JSON data.

If you use Java RESTful web service frameworks, such as JAX-RS, for building RESTful web APIs,
the serialization and deserialization of the request and response messages will be taken care of by the
framework.

The role of the JSON marshalling and unmarshalling components in a
typical Java RESTful web service implementation:

![jax](https://github.com/vgorbic1/Tutorials/blob/master/Web%20Services/images/jax.jpg)

Two widely adopted programming
models for processing JSON are as follows:
- **Object model**: In this model, the entire JSON data is read into memory in a tree format. This
tree can be traversed, analyzed, or modified with the appropriate APIs. As this approach loads
the entire content into the memory first and then starts parsing, it ends up consuming more
memory and CPU cycles. However, this model gives more flexibility while manipulating the
content.
- **Streaming model**: The term streaming means that data can be read or written in blocks. This model
does not read the entire JSON content into the memory to get started with parsing; rather, it reads
one element at a time. For each token read, the parser generates appropriate events indicating the
type of token, such as the start or end of an array, or the start or end of the object and attribute
values. A client can process the contents by listening for appropriate events. The most important
point is that instead of letting the parser push the content to the client (push parser), the client can
pull the information from the parser as it needs (pull parser). In this model, the client is allowed
to skip or stop reading contents in the middle of the process if it has finished reading the desired
elements. This model is also useful when you write contents to an output source in blocks.

You may want to consider using streaming APIs in the following situations:
- When the data is huge in size and it is not feasible to load the entire content into the memory for
processing the content
- When the partial processing is needed and the data model is not fully available yet
