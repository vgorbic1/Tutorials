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
