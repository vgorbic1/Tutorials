## WSDL
WSDL stands for Web Services Description Language. It is the standard format for describing a web service. WSDL was developed jointly by Microsoft and IBM. WSDL is often used in combination with SOAP and XML Schema to provide web services over the Internet. A client program connecting to a web service can read the WSDL to determine what functions are available on the server. Any special datatypes used are embedded in the WSDL file in the form of XML Schema. The client can then use SOAP to actually call one of the functions listed in the WSDL. 

WSDL breaks down web services into three specific, identifiable elements that can be combined or reused once defined. The three major elements of WSDL that can be defined separately are:
- Types
- Operations
- Binding

A WSDL document has various elements, but they are contained within these three main elements, which can be developed as separate documents and then they can be combined or reused to form complete WSDL files.

#### Elements
WSDL parts are usually generated automatically using web services-aware tools.
- **Definition** It is the root element of all WSDL documents. It defines the name of the web service, declares multiple namespaces used throughout the remainder of the document, and contains all the service elements described here.
- **Data types** The data types to be used in the messages are in the form of XML schemas.
- **Message** It is an abstract definition of the data, in the form of a message presented either as an entire document or as arguments to be mapped to a method invocation.
- **Operation** It is the abstract definition of the operation for a message, such as naming a method, message queue, or business process, that will accept and process the message.
- **Port type** It is an abstract set of operations mapped to one or more end-points, defining the collection of operations for a binding; the collection of operations, as it is abstract, can be mapped to multiple transports through various bindings.
- **Binding** It is the concrete protocol and data formats for the operations and messages defined for a particular port type.
- **Port** It is a combination of a binding and a network address, providing the target address of the service communication.
- **Service** It is a collection of related end-points encompassing the service definitions in the file; the services map the binding to the port and include any extensibility definitions.
- **Documentation** This element is used to provide human-readable documentation and can be included inside any other WSDL element.
- **Import** This element is used to import other WSDL documents or XML Schemas.

The main structure of a WSDL document looks like this:
```xml
<definitions>
   <types>
      definition of types........
   </types>

   <message>
      definition of a message....
   </message>

   <portType>
      <operation>
         definition of a operation.......  
      </operation>
   </portType>

   <binding>
      definition of a binding....
   </binding>

   <service>
      definition of a service....
   </service>
</definitions>
```

#### Example
Let us assume the service provides a single publicly available function, called sayHello. This function expects a single string parameter and returns a single string greeting. For example, if you pass the parameter world then service function sayHello returns the greeting, "Hello, world!". Contents of HelloService.wsdl file:
```xml
<definitions name="HelloService"
   targetNamespace="http://www.examples.com/wsdl/HelloService.wsdl"
   xmlns="http://schemas.xmlsoap.org/wsdl/"
   xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/"
   xmlns:tns="http://www.examples.com/wsdl/HelloService.wsdl"
   xmlns:xsd="http://www.w3.org/2001/XMLSchema">
 
   <message name="SayHelloRequest">
      <part name="firstName" type="xsd:string"/>
   </message>
	
   <message name="SayHelloResponse">
      <part name="greeting" type="xsd:string"/>
   </message>

   <portType name="Hello_PortType">
      <operation name="sayHello">
         <input message="tns:SayHelloRequest"/>
         <output message="tns:SayHelloResponse"/>
      </operation>
   </portType>

   <binding name="Hello_Binding" type="tns:Hello_PortType">
      <soap:binding style="rpc"
         transport="http://schemas.xmlsoap.org/soap/http"/>
      <operation name="sayHello">
         <soap:operation soapAction="sayHello"/>
         <input>
            <soap:body
               encodingStyle="http://schemas.xmlsoap.org/soap/encoding/"
               namespace="urn:examples:helloservice"
               use="encoded"/>
         </input>
		
         <output>
            <soap:body
               encodingStyle="http://schemas.xmlsoap.org/soap/encoding/"
               namespace="urn:examples:helloservice"
               use="encoded"/>
         </output>
      </operation>
   </binding>

   <service name="Hello_Service">
      <documentation>WSDL File for HelloService</documentation>
      <port binding="tns:Hello_Binding" name="Hello_Port">
         <soap:address
            location="http://www.examples.com/SayHello/" />
      </port>
   </service>
</definitions>
```
