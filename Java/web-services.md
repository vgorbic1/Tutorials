## Java Web Services
There are two main API's defined by Java for developing web service applications since JavaEE 6.
- **JAX-WS**: for SOAP web services. The are two ways to write JAX-WS application code: by RPC style and Document style.
- **JAX-RS**: for RESTful web services. There are mainly 2 implementation currently in use for creating JAX-RS application: Jersey and RESTeasy.

#### JAX-WS
There are two ways to develop JAX-WS example: RPC style and Document style.

**RPC Style**

RPC style web services use method name and parameters to generate XML structure.
- The generated WSDL is difficult to be validated against schema.
- In RPC style, SOAP message is sent as many elements.
- RPC style message is tightly coupled.
- In RPC style, SOAP message keeps the operation name.
- In RPC style, parameters are sent as discrete values.

*WSDL file:*

In WSDL file, it doesn't specify the types details: `<types/>`

*Message part*
```xml
<message name="getHelloWorldAsString">  
<part name="arg0" type="xsd:string"/>  
</message>  
<message name="getHelloWorldAsStringResponse">  
<part name="return" type="xsd:string"/>  
</message>  
```
*Soap:body*
```xml
<binding name="HelloWorldImplPortBinding" type="tns:HelloWorld">  
<soap:binding transport="http://schemas.xmlsoap.org/soap/http" style="rpc"/>  
<operation name="getHelloWorldAsString">  
<soap:operation soapAction=""/>  
<input>  
<soap:body use="literal" namespace="http://javatpoint.com/"/>  
</input>  
<output>  
<soap:body use="literal" namespace="http://javatpoint.com/"/>  
</output>  
</operation>  
</binding>  
```
[EXAMPLE](http://www.javatpoint.com/jax-ws-example-rpc-style)

**Document Style**

- Document style web services can be validated against predefined schema.
- In document style, SOAP message is sent as a single document.
- Document style message is loosely coupled.
- In Document style, SOAP message loses the operation name.
- In Document style, parameters are sent in XML format.

*WSDL file:*
```xml
<types>  
<xsd:schema>  
<xsd:import namespace="http://javatpoint.com/" schemaLocation="http://localhost:7779/ws/hello?xsd=1"/>  
</xsd:schema>  
</types>  
```
*Message part*
```xml
<message name="getHelloWorldAsString">  
<part name="parameters" element="tns:getHelloWorldAsString"/>  
</message>  
<message name="getHelloWorldAsStringResponse">  
<part name="parameters" element="tns:getHelloWorldAsStringResponse"/>  
</message>  
```
*Soap:body*
```xml
<binding name="HelloWorldImplPortBinding" type="tns:HelloWorld">  
<soap:binding transport="http://schemas.xmlsoap.org/soap/http" style="document"/>  
<operation name="getHelloWorldAsString">  
<soap:operation soapAction=""/>  
<input>  
<soap:body use="literal"/>  
</input>  
<output>  
<soap:body use="literal"/>  
</output>  
</operation>  
</binding>  
```
[EXAMPLE](http://www.javatpoint.com/jax-ws-example-document-style)

#### JAX-RS
There are two main implementation of JAX-RS API: Jersey and RESTEasy.

Jersey: [EXAMPLE](http://www.javatpoint.com/jax-rs-example-jersey)

Annotations: [EXAMPLE](http://www.javatpoint.com/jax-rs-annotations-example)

JAX-RS File Download: [EXAMPLE](http://www.javatpoint.com/jax-rs-file-download-example)

JAX-RS File Upload: [EXAMPLE](http://http://www.javatpoint.com/jax-rs-file-upload-example)

#### Web Services Interview Questions
*What is Web Service?*

Web Service is a software system for communicating two devices over the network.

*What are the advantages of web services?*
By the help of web services, an application can communicate with other application developed in any language. We can expose the web service so that other applications can use it. We can create a service for a specific task such as tax calculation etc.

*What are the different types of web services?*

There are two types of web services: SOAP and RESTful.

*What is SOAP?*

SOAP stands for Simple Object Access Protocol. It is a XML-based protocol for accessing web services.

*What are the advantages of SOAP web services?*

SOAP has WS security, language independent, platform Independent

*What are the disadvantages of SOAP web services?*

SOAP is slower than RESTful and WSDL dependent.

*What is WSDL?*

WSDL stands for Web Services Description Language. It is a xml document containing information about web services such as method name, method parameter etc. 

*What is RESTful web services?*

REST stands for REpresentational State Transfer. It is a architectural style. It is not a protocol like SOAP.

*What are the advantages of RESTful web services?*

RESTful is fast, language independent, platform independent, can use SOAP, allows different data formats.

*What is SOA?*

SOA stands for Service Oriented Architecture. It is a design pattern to provide services to other application through protocol. 

*What tools are used to test web services?*

- SoapUI tool for testing SOAP and RESTful web services.
- Poster for Firefox browser.
- Postman extension for Chrome browser.

[SOURCE](http://www.javatpoint.com/web-services-interview-questions)
