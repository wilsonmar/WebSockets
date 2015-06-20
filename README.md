This mark-down text page and associated solution files demonstrates how to program and performance test
HTTP5 WebSocket implemented in Visual Studio and the C# language versus other competing technologies.

## <a name="Why"> Why WebSockets?</a>
Web Sockets is popular now because:
* its HTTP headers take less bytes than HTTP 
* data exchanged is more compact than JSON.
* it enables **two-way** communication, so pages automatically refresh without user action (thus "real time").

This means that it's faster and more "user friendly" than REST API and forms technologies that preceded it.

WebSockets as described on MDN:
  * https://developer.mozilla.org/en-US/docs/WebSockets/Writing_WebSocket_client_applications

By its nature it's a full-duplex **asychronous** protocol.


### <a name="MS_WebSockets"> Microsoft Web Sockets</a>
To implement Web Sockets Microsoft offers its SignalR library (at http://SignalR.net)
for addition to all ASP.NET project types (MVC).

  * http://www.pluralsight.com/courses/one-aspdotnet-from-scratch
  demostrates how to create a SignalR "ChatHub" app updates the user count on all browser instances automatically
  as browser instances are added and disengaged.
  
  * http://shooter.signalr.net provides a demo app written in HTML using SignalR.
  
 * HTML5 Web Sockets - http://social.technet.microsoft.com/wiki/contents/articles/7148.websockets-in-asp-net.aspx


### <a name="LightStreamer"> Java-based LightStreamer</a>
There is a commercial product (with an open-source free version)
that provides so many more sophisticated features that make other implementations seem like "toys". 

It is programmed in Java.

