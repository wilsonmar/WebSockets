This mark-down text page and associated solution files demonstrates how to program and performance test
HTTP5 WebSocket implemented in Visual Studio and the C# language versus other competing technologies.

## <a name="Why"> Why WebSockets?</a>
Web Sockets is gaining popularity now (in 2015) because:
* its HTTP headers take less bytes than HTTP 
* payload data exchanged is more compact than JSON.

This lighterweight and low-latency 
means that it's faster and processes more transactions than the same hardware
than REST API and forms technologies that preceded it.

Websockets are also more "user friendly" 
because it enables **two-way** communication, so pages automatically refresh without user action.

WebSockets is a persistant but volatile connection, 
not a "durable" connection like those provided by MQ (message queues).

By its nature it's a full-duplex **asychronous** protocol.

Web sockets provide push within the applications, such a used by "real-time" feeds such as 
stock and sports tickers, on-line gaming, etc.
Web sockets techonology is also used for communication between two servers without a human UI.

WebSockets provides a quicker user experience than the "long polling" programming approach used in

 * http://www.bitcoinmonitor.com/ which displays real-time trades over time.
 * http://pokein.com/ integrates a DLL in a .NET project as well.
 * http://www.frozenmountain.com/websync/
 * Asana for task collaboration (developed by people from Facebook)

 
 
<hr />


### <a name="DemoApps"> Demo Apps</a>
There are several examples with coding that created it:

 * https://jabbr.net
  was written using <a href="#SignalR"> Microsoft ASP.NET SignalR</a>.

 * http://shooter.signalr.net provides a demo app written in HTML using 
  <a href="#SignalR">SignalR</a>.

Code for demos downloaded and run in your localhost:

* http://nuget.org/packages/Microsoft.AspNet.SignalR.Sample
 provides a sample SignalR stock ticker solution built using
  <a href="#SignalR">SignalR</a>.
 It is installed in the Package Manager Console.
 Its dependencies include JQuery and Owin.

* Tutorial http://www.pluralsight.com/courses/signalr-introduction
 by Christian Weyer (@christianweyer) at http://www.thinkecture.com 
 describes the student list demo app at
 codeplex?

* http://github.com/cbeams/bitcoin-rt
 is described by the author Chris Beams in a video at https://www.youtube.com/watch?v=z-CYO1ABCp4&t=8m44s
 by SpringSource (a VMware company).
 using node.js, SockJS, and the D3.js library instead of jQuery UI.

 The Java implementation uses Java Tomcat native WebSocket API, Atmosphere, and Vert.x libraries.

### <a name="RealTimeTech"> Real-Time Technologies</a>
A list of real-time technologies (which include WebSockets) is at
http://www.leggetter.co.uk/real-time-web-technologies-guide/

### <a name="Pusher"> Pusher.com</a>
It's maintained by  is maintained by Phil Leggetter from 
Pusher.com is a paid service for web application developers that handles the burden of delivering real-time updates to potentially millions of users and applications at once.



### <a name="JavaFirst"> Java Origins</a>
Because the JSR-356 deliver a Java API in Java EE 7,
the first implementations of WebSockets were in the Java language.

Tutorials in the Java language include:
 * https://www.youtube.com/watch?v=z-CYO1ABCp4 by 

 * http://kaazing.com/ see http://blog.kaazing.com/2011/11/17/the-industrys-best-websocket-emulation-real-time-web-apps-for-all-your-customers-even-if-theyre-on-ie6/ by Peter Moskovitz
 
 * http://superwebsocket.codeplex.com/
 * http://xsockets.net/
 * Autobahn WebSockets, a high-performance WS server that supports Windows 
   running on top of IOCP (I/O completion ports) in order to scale to large connection numbers (hundred thousands).
   http://stackoverflow.com/users/884770/oberstet

### <a name="DataExchange"> Data Exchange Details</a>
DO THIS:
Use Fiddler2 to examine packets.

WebSockets is an IETF standard http://ietf.org/rfc/rfc6455.txt
standardized by the W3C
as described on MDN:
  * https://developer.mozilla.org/en-US/docs/WebSockets/Writing_WebSocket_client_applications

WebSockets is not the **"push notification"** technology as what operating systems provide.

WebSockets is not the persistent publish-subscribe design pattern since it's temporary to a particular session.

WebSockets begins by doing an "upgrade" to the HTTP protocol.
If a client can do it, it responds with a HTTP 101 response code (rather than 400).


### <a name="LightStreamer"> Java-based LightStreamer</a>
There is a commercial product (with an open-source free version)
that provides so many more sophisticated features that make other implementations seem like "toys". 

It is programmed in Java.

### <a name="NodeJS"> NodeJS Implementations</a>
The Socket.io module for Node.js


### <a name="SignalR"> Microsoft Web Sockets SignalR</a>
To implement Web Sockets Microsoft offers its SignalR library 
described at http://SignalR.net and stored as open-source repo at
http://github.com/Microsoft/SignalR.

See http://www.wikiwand.com/en/SignalR

SignalR packages available via NuGet at
http://nuget.org/packages/Microsoft.AspNet.SignalR

SignalR can be added to all ASP.NET project types (MVC).

The **Microsoft.AspNet.SignalR** library brings in everything to run on IIS and ASP.NET
within Windows 2012/Windows 8 and newer machines.
Thus it is not common in production yet in 2015.

The Microsoft.AspNet.SignalR.SystemWeb library provides components to use OWIN ASP.NET host.

The Microsoft.AspNet.SignalR.Core library provides components to build SignalR endpoints.

Its Microsoft.AspNet.SignalR.Client library enables the server to work with clients programmed in
WinRT, Windows Phone 8, and Sliverlight5.
Its Microsoft.AspNet.SignalR.Js library enables the server to work with clients programmed in JQuery.

The Microsoft.AspNet.SignalR.Utils library provides command-line utilities to install performance counters
and generate Hub JavaScript proxies.

SignalR is supported 

  * http://www.pluralsight.com/courses/one-aspdotnet-from-scratch
  demostrates how to create a SignalR "ChatHub" app updates the user count on all browser instances automatically
  as browser instances are added and disengaged.
  
QUESTION:
Does SignalR support Websockets sub-protocols?

### <a name="SignalRHubs"> Hubs in Microsoft Web Sockets SignalR</a>
**Hubs** programming model 
in a RPC-ish style of URLs.


### <a name="BenchmarkStudies"> Benchmark Studies</a>
Comparison of Comet vs. WebSockets technologies at
http://webtide.intalio.com/2011/09/cometd-2-4-0-websocket-benchmarks/
found an over 150x factor in favor of WebSockets (700ms vs. 3 ms at 50,000 users).


## <a name="References"> References</a>
 * HTML5 Web Sockets - http://social.technet.microsoft.com/wiki/contents/articles/7148.websockets-in-asp-net.aspx
