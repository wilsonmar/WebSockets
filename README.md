This mark-down text page and associated solution files demonstrates how to program and performance test
HTTP5 WebSocket implemented in Visual Studio and the C# language versus other competing technologies.

## <a name="Why"> Why WebSockets?</a>
Web Sockets is gaining popularity now (in 2015) because:
* its HTTP headers take less bytes than HTTP 
* data exchanged is more compact than JSON.

This lighter weight means that it's faster and processes more transactions than the same hardware
than REST API and forms technologies that preceded it.

Websockets are also more "user friendly" 
because it enables **two-way** communication, so pages automatically refresh without user action.

By its nature it's a full-duplex **asychronous** protocol.

Web Sockets is not the **"push notification"** technology as what operating systems provide.

Web sockets provide push within the applications, such a used by "real-time" feeds such as 
stock and sports tickers, on-line gaming, etc.
Web sockets techonology is also used for communication between two servers without a human UI.

WebSockets as described on MDN:
  * https://developer.mozilla.org/en-US/docs/WebSockets/Writing_WebSocket_client_applications


<hr />


### <a name="DemoApps"> Demo Apps</a>
There are several examples with coding that created it:

* Tutorial http://www.pluralsight.com/courses/signalr-introduction
 by Christian Weyer (@christianweyer) at http://www.thinkecture.com 
 describes the student list demo app at
 codeplex?


### <a name="LightStreamer"> Java-based LightStreamer</a>
There is a commercial product (with an open-source free version)
that provides so many more sophisticated features that make other implementations seem like "toys". 

It is programmed in Java.

### <a name="MS_WebSockets"> Microsoft Web Sockets</a>
To implement Web Sockets Microsoft offers its SignalR library (at http://SignalR.net)
for addition to all ASP.NET project types (MVC).

  * http://www.pluralsight.com/courses/one-aspdotnet-from-scratch
  demostrates how to create a SignalR "ChatHub" app updates the user count on all browser instances automatically
  as browser instances are added and disengaged.
  
  * http://shooter.signalr.net provides a demo app written in HTML using SignalR.
  
 * HTML5 Web Sockets - http://social.technet.microsoft.com/wiki/contents/articles/7148.websockets-in-asp-net.aspx

