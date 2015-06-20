This mark-down text page and associated solution files demonstrates how to program and performance test
HTTP5 WebSocket implemented in Visual Studio and the C# language versus other competing technologies.

## <a name="Why"> Why WebSockets?</a>
Web Sockets is gaining popularity now (in 2015) because:
* its HTTP headers take less bytes than HTTP 
* data exchanged is more compact than JSON.

This lighterweight and low-latency 
means that it's faster and processes more transactions than the same hardware
than REST API and forms technologies that preceded it.

Websockets are also more "user friendly" 
because it enables **two-way** communication, so pages automatically refresh without user action.

By its nature it's a full-duplex **asychronous** protocol.

Web sockets provide push within the applications, such a used by "real-time" feeds such as 
stock and sports tickers, on-line gaming, etc.
Web sockets techonology is also used for communication between two servers without a human UI.

WebSockets is an IETF standard http://ietf.org/rfc/rfc6455.txt
standardized by the W3C
as described on MDN:
  * https://developer.mozilla.org/en-US/docs/WebSockets/Writing_WebSocket_client_applications

WebSockets is not the **"push notification"** technology as what operating systems provide.

WebSockets is not the persistent publish-subscribe design pattern since it's temporary to a particular session.

WebSockets begins by doing an "upgrade" to the HTTP protocol.
If a client can do it, it responds with a HTTP 101 response code (rather than 400).

<hr />


### <a name="DemoApps"> Demo Apps</a>
There are several examples with coding that created it:

* Tutorial http://www.pluralsight.com/courses/signalr-introduction
 by Christian Weyer (@christianweyer) at http://www.thinkecture.com 
 describes the student list demo app at
 codeplex?

### <a name="JavaFirst"> Java Origins</a>
Because the JSR-356 deliver a Java API in Java EE 7,
the first implementations of WebSockets were in the Java language.

Tutorials in the Java language include:
 * https://www.youtube.com/watch?v=z-CYO1ABCp4 by 
   SpringSource (a VMware company).

### <a name="LightStreamer"> Java-based LightStreamer</a>
There is a commercial product (with an open-source free version)
that provides so many more sophisticated features that make other implementations seem like "toys". 

It is programmed in Java.

### <a name="NodeJS"> NodeJS Implementations</a>


### <a name="MS_WebSockets"> Microsoft Web Sockets</a>
To implement Web Sockets Microsoft offers its SignalR library (at http://SignalR.net)
for addition to all ASP.NET project types (MVC).

  * http://www.pluralsight.com/courses/one-aspdotnet-from-scratch
  demostrates how to create a SignalR "ChatHub" app updates the user count on all browser instances automatically
  as browser instances are added and disengaged.
  
  * http://shooter.signalr.net provides a demo app written in HTML using SignalR.
  
 * HTML5 Web Sockets - http://social.technet.microsoft.com/wiki/contents/articles/7148.websockets-in-asp-net.aspx

