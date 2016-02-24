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
