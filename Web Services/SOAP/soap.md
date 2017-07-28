## SOAP
SOAP is an acronym for Simple Object Access Protocol. It is an XML-based messaging protocol for exchanging information among computers. Although SOAP can be used in a variety of messaging systems and can be delivered via a variety of transport protocols, the initial focus of SOAP is remote procedure calls transported via HTTP. Other frameworks including CORBA, DCOM, and Java RMI provide similar functionality to SOAP, but SOAP messages are written entirely in XML and are therefore uniquely platform- and language-independent.

## Message Structure
A SOAP message is an ordinary XML document containing the following elements:
- **Envelope** Defines the start and the end of the message. It is a mandatory element.
- **Header** Contains any optional attributes of the message used in processing the message, either at an intermediary point or at the ultimate end-point. It is an optional element.
- **Body** Contains the XML data comprising the message being sent. It is a mandatory element.
- **Fault** An optional Fault element that provides information about errors that occur while processing the message.
```xml
<?xml version="1.0"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://www.w3.org/2001/12/soap-envelope" SOAP-ENV:encodingStyle="http://www.w3.org/2001/12/soap-encoding">

   <SOAP-ENV:Header>
   </SOAP-ENV:Header>
   
   <SOAP-ENV:Body>
      <SOAP-ENV:Fault>
         ...
         ...
      </SOAP-ENV:Fault>
   </SOAP-ENV:Body>
   
</SOAP_ENV:Envelope>
```

#### Envelope
The SOAP envelope indicates the start and the end of the message so that the receiver knows when an entire message has been received. The SOAP envelope solves the problem of knowing when you are done receiving a message and are ready to process it. The SOAP envelope is therefore basically a packaging mechanism.
- Every SOAP message has a root Envelope element.
- Envelope is a mandatory part of SOAP message.
- Every Envelope element must contain exactly one Body element.
- If an Envelope contains a Header element, it must contain no more than one, and it must appear as the first child of the Envelope, before the Body.
- The envelope changes when SOAP versions change.
- The SOAP envelope is specified using the ENV namespace prefix and the Envelope element.
- The optional SOAP encoding is also specified using a namespace name and the optional encodingStyle element, which could also point to an encoding style other than the SOAP one.
- A v1.1-compliant SOAP processor generates a fault upon receiving a message containing the v1.2 envelope namespace.
- A v1.2-compliant SOAP processor generates a VersionMismatch fault if it receives a message that does not include the v1.2 envelope namespace.
The following example illustrates the use of a SOAP message within an HTTP POST operation, which sends the message to the server:
```xml
POST /OrderEntry HTTP/1.1
Host: www.tutorialspoint.com
Content-Type: application/soap;  charset="utf-8"
Content-Length: nnnn
<?xml version="1.0"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://www.w3.org/2001/12/soap-envelope" SOAP-ENV:encodingStyle=" http://www.w3.org/2001/12/soap-encoding">
   ... Message information goes here ...
</SOAP-ENV:Envelope>
```

#### Header
The optional Header element offers a flexible framework for specifying additional application-level requirements. For example, the Header element can be used to specify a digital signature for password-protected services. Likewise, it can be used to specify an account number for pay-per-use SOAP services.
- Header elements can occur multiple times.
- Headers are intended to add new features and functionality.
- The SOAP header contains header entries defined in a namespace.
- The header is encoded as the first immediate child element of the SOAP envelope.
- When multiple headers are defined, all immediate child elements of the SOAP header are interpreted as SOAP header blocks.

A SOAP Header can have the following two attributes:
- **Actor** attribute
The SOAP protocol defines a message path as a list of SOAP service nodes. Each of these intermediate nodes can perform some processing and then forward the message to the next node in the chain. By setting the Actor attribute, the client can specify the recipient of the SOAP header.
- **MustUnderstand** attribute
It indicates whether a Header element is optional or mandatory. If set to true, the recipient must understand and process the Header attribute according to its defined semantics, or return a fault.
```xml
<?xml version="1.0"?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV=" http://www.w3.org/2001/12/soap-envelope" SOAP-ENV:encodingStyle=" http://www.w3.org/2001/12/soap-encoding">
   <SOAP-ENV:Header>
      <t:Transaction xmlns:t="http://www.tutorialspoint.com/transaction/" SOAP-ENV:mustUnderstand="true">5</t:Transaction>
   </SOAP-ENV:Header>
   ...
</SOAP-ENV:Envelope>
```

#### Body
The SOAP body is a mandatory element that contains the application-defined XML data being exchanged in the SOAP message. The body must be contained within the envelope and must follow any headers that might be defined for the message.
The body contains mandatory information intended for the ultimate receiver of the message. For example:
```xml
<?xml version="1.0"?>
<SOAP-ENV:Envelope>
 ...
   <SOAP-ENV:Body>
      <m:GetQuotation xmlns:m="http://www.tp.com/Quotation">
         <m:Item>Computers</m:Item>
      </m:GetQuotation>
   </SOAP-ENV:Body>
...
</SOAP-ENV:Envelope>
```
The example above requests a quotation of computer sets. Note that the m:GetQuotation and the Item elements above are application-specific elements. They are not a part of the SOAP standard. Here is the response to the above query:
```xml
<?xml version="1.0"?>
<SOAP-ENV:Envelope>
 ...
   <SOAP-ENV:Body>
      <m:GetQuotationResponse xmlns:m="http://www.tp.com/Quotation">
         <m:Quotation>This is Qutation</m:Quotation>
      </m:GetQuotationResponse>
   </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```
Normally, the application also defines a schema to contain semantics associated with the request and response elements.

#### Fault
If an error occurs during processing, the response to a SOAP message is a SOAP fault element in the body of the message, and the fault is returned to the sender of the SOAP message. The SOAP fault mechanism returns specific information about the error, including a predefined code, a description, and the address of the SOAP processor that generated the fault.
- A SOAP message can carry only one fault block.
- Fault is an optional part of a SOAP message.
- For HTTP binding, a successful response is linked to the 200 to 299 range of status codes.
- SOAP Fault is linked to the 500 to 599 range of status codes.
The following code is a sample Fault. The client has requested a method named ValidateCreditCard, but the service does not support such a method. This represents a client request error, and the server returns the following SOAP response:
```xml
<?xml version='1.0' encoding='UTF-8'?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/1999/XMLSchema-instance" xmlns:xsd="http://www.w3.org/1999/XMLSchema">
   <SOAP-ENV:Body>
      <SOAP-ENV:Fault>
         <faultcode xsi:type="xsd:string">SOAP-ENV:Client</faultcode>
         <faultstring xsi:type="xsd:string">
            Failed to locate method (ValidateCreditCard) in class (examplesCreditCard) at /usr/local/ActivePerl-5.6/lib/site_perl/5.6.0/SOAP/Lite.pm line 1555.
         </faultstring>
      </SOAP-ENV:Fault>
   </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```

#### Encoding
SOAP includes a built-in set of rules for encoding data types. It enables the SOAP message to indicate specific data types, such as integers, floats, doubles, or arrays.SOAP data types are divided into two broad categories − scalar types and compound types. 
- **Scalar types** contain exactly one value such as a last name, price, or product description. For scalar types, SOAP adopts all the built-in simple types specified by the XML Schema specification. This includes strings, floats, doubles, and integers. Compound types contain multiple values such as a purchase order or a list of stock quotes. SOAP response with a double data type:
```xml
<?xml version='1.0' encoding='UTF-8'?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://www.w3.org/2001/12/soap-envelope" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
   <SOAP-ENV:Body>
      <ns1:getPriceResponse xmlns:ns1="urn:examples:priceservice"  SOAP-ENV:encodingStyle="http://www.w3.org/2001/12/soap-encoding">
         <return xsi:type="xsd:double">54.99</return>
      </ns1:getPriceResponse>
   </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```
- Compound types are further subdivided into arrays and structs. SOAP response with an array of double values:
```xml
<?xml version='1.0' encoding='UTF-8'?>
<SOAP-ENV:Envelope xmlns:SOAP-ENV="http://www.w3.org/2001/12/soap-envelope" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
   <SOAP-ENV:Body>
      <ns1:getPriceListResponse xmlns:ns1="urn:examples:pricelistservice"  SOAP-ENV:encodingStyle="http://www.w3.org/2001/12/soap-encoding">
         <return xmlns:ns2="http://www.w3.org/2001/09/soap-encoding"  xsi:type="ns2:Array" ns2:arrayType="xsd:double[2]">
            <item xsi:type="xsd:double">54.99</item>
            <item xsi:type="xsd:double">19.99</item>
         </return>
      </ns1:getPriceListResponse>
   </SOAP-ENV:Body>
</SOAP-ENV:Envelope>
```
