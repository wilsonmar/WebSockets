This mark-down text page and associated solution files demonstrates how to program and performance test
HTTP5 WebSocket implemented in Visual Studio and the C# language versus other competing technologies.

Applications such as stock and sports tickers, on-line gaming, etc.
used various techniques to provide "real-time" updates without the need for users to manually refresh the screen
or click a button. 

### <a name="ObserveRealTimeTech"> Observe Older Real-Time Technologies</a>
1). Open a browser which does not support WebSockets, such as Internet Explorer 8.

2). Press F12 to Trace the HTTP packets involved.

3). Specify one of these publicly available websites:

 * http://www.bitcoinmonitor.com/ which displays real-time trades over time.
 * http://pokein.com/ integrates a DLL in a .NET project.
 * http://www.frozenmountain.com/websync/
 * Asana for task collaboration (developed by people from Facebook)

4). Notice that this approach is rather "chatty".


## <a name="Why"> Why WebSockets?</a>
Web Sockets is gaining popularity now (in 2015) because:
  * its HTTP headers take less bytes than HTTP 
  * payload data exchanged is more compact than JSON.

This lighterweight and low-latency 
means that it's faster and processes more transactions than the same hardware
than REST API and forms technologies that preceded it.

Websockets are also more "user friendly" 
because it enables **two-way** communication, so pages automatically refresh without user action
through a persistant but volatile connection, 
not a "durable" connection like those provided by MQ (message queues).

By its nature it's a full-duplex **asychronous** protocol.

WebSockets is not the **"push notification"** technology as what operating systems provide.

WebSockets is not the persistent publish-subscribe design pattern since it's temporary to a particular session.


### <a name="JavaFirst"> Java Origins</a>
Because the JSR-356 deliver a Java API in Java EE 7,
the first implementations of WebSockets were in the Java language.

* http://github.com/cbeams/bitcoin-rt
 is described by the author Chris Beams in a video at https://www.youtube.com/watch?v=z-CYO1ABCp4&t=8m44s
 by SpringSource (a VMware company).
 using node.js, SockJS, and the D3.js library instead of jQuery UI.
(The Java implementation uses Java Tomcat native WebSocket API, Atmosphere, and Vert.x libraries.)


Tutorials in the Java language include:
 * https://www.youtube.com/watch?v=z-CYO1ABCp4 by 

 * http://kaazing.com/ see http://blog.kaazing.com/2011/11/17/the-industrys-best-websocket-emulation-real-time-web-apps-for-all-your-customers-even-if-theyre-on-ie6/ by Peter Moskovitz
 
 * http://superwebsocket.codeplex.com/
 * http://xsockets.net/
 * Autobahn WebSockets, a high-performance WS server that supports Windows 
   running on top of IOCP (I/O completion ports) in order to scale to large connection numbers (hundred thousands).
   http://stackoverflow.com/users/884770/oberstet



### <a name="DemoApps"> Demo Apps</a>
1). Open a modern browser 

2). Press F12 to Trace the HTTP packets involved.

3). Specify the URL of one of these demo sites created using WebSockets technology:

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

 In the tutorial he uses VisualStudio 2012 to show 
 <a href="#SimpleChat">construciton of a simple real-time chat program</a>.




### <a name="Negotiation"> Fall-back Negotiation</a>
4). In the **web.config** file, specify a version that does not support WebSockets SignalR:

```
<httpRunTime targetFramework="4.0">
```

The first version that supports SignalR is **4.5**.

5). Reload the web page so the client sends an initial request to the server, 
the **negotiate** request.

The JSON response contains
  * ConnectionId
  * ConnectionToken
  * DisconnectTimeout
  * ProtocolVersion
  * TryWebSockets
  * Url
  * WebSocketUrl (no longer used)

WebSockets is an IETF standard http://ietf.org/rfc/rfc6455.txt
standardized by the W3C
as described on MDN:
  * https://developer.mozilla.org/en-US/docs/WebSockets/Writing_WebSocket_client_applications


6). Look at the JavaScript Console

If the client does not support WebSockets, it responds with **500 HTTP status**,
which is the standard response.

Newer WebSockets technologies **fall back** to these in the sequence shown.

### <a name="RealTimeTech"> Older Real-Time Technologies</a>
Before WebSockets, programmers "hacked" ways 
Web sockets techonology is also used for communication between two servers without a human UI.
In order of preference:

   1. Server Sent Event (SSE)
   2. "Forever Frame"
   3. "Long Polling"

A list of real-time technologies (which include WebSockets) is at
http://www.leggetter.co.uk/real-time-web-technologies-guide/
maintained by by Phil Leggetter, the Technical Evangelist at 
Pusher.com, a paid service for web application developers that handles the burden of delivering real-time updates to many users and applications at once.

### <a name="RealTimeTech"> Older Real-Time Technologies</a>

7). In the **web.config** file, specify a version that supports WebSockets SignalR:

```
<httpRunTime targetFramework="4.5">
```

8). Refresh the page.

Notice in the JavaScript Console "WebSocket opened".

### <a name="BrowserUpgrade"> Browser Upgrade</a>

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

Katana (from http://katanaproject.codeplex.com/documentation)
is a set of components for building and running Web applications on a common hosting abstraction. 
The hosting abstraction is OWIN (Open Web Interface for .NET) programming model for developers.
IIS is a process manager. OwinHost is a standalone executable that can start up an OWIN application. The new thing is WebListener which is ultra light-weight server component where you can expect pretty amazing performance results. 
See http://www.techbubbles.com/aspnet/what-is-katana-and-owin-for-asp-net/

http://katanaproject.codeplex.com/

https://github.com/owin/museum-piece-owin-hosting

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

### <a name="SimpleChat"> Construciton of a simple real-time chat program</a>.
1). Open Visual Studio 2012.

2). Create a MVC 4 Web product solution named SimpleChat.
 This establishes ASP.NET Controllers and App_Start files WebApiConfig.cs, FilterConfig.cs, and RouteConfig.cs.

3). In Solution Explorer, right-click on the project and press Ctrl+Shift+A to Add New Item **SignalR Hub Class**.

<a target="_blank" href="https://cloud.githubusercontent.com/assets/300046/8270037/a4ef6abe-1785-11e5-8a93-a6c13f050931.png">
<img align="right" src="https://cloud.githubusercontent.com/assets/300046/8270037/a4ef6abe-1785-11e5-8a93-a6c13f050931.png"
width="350" /></a>
4). Name it "ChatHub.cs".
 
 NuGet obtains over the internet various dependency packages, listed under the project's References.

 The dependencies include http://owin.org/ and the Newtonsoft assembly and package.

5). Define a name attribute for check-in to the public API:

```
[HubName(chat)]
```

This makes use of Microsoft.AspNet.SignalR.Hubs;

6). Instead of the default `public void Hello()`

```
 public void SendMessage(string message){
     Clients.All.hello();
 }
```

 This sends a string to all clients.

7). In Global.aspx, add before the RouteConfig line:

```
RouteTable.Route.MapHubs();
```

8). Recompile and use URL that includes the base endpoint default name of "signalr".

```
http://localhost:???/signalr/hubs
```

which returns the JavaScript library downloaded by client browsers.

9). In ChatHub.cs add a call to send a complex type:

```
public void SendMessageData(SendDate message)
```

10). Right-click on the line and select Create Class and insert in it:

```
public int Id { get; set; }
public string Data { get; set; }
```

11). Add an async call task type:

```
public Task<int> SendDataAsync() {
```



serialized into and deserialized from JSON (using the JSON.NET library).

Like other ASP.NET (such as MVC), first define a **route** in the host process definition code.
???

in a RPC-ish style of URLs.

Upon connection (such as opening a new browser window) ...

Upon disconnection (such as closing of a browser window) ....

Grouping ...


### <a name="BenchmarkStudies"> Benchmark Studies of Efficiency and Scalability</a>
Comparison of Comet vs. WebSockets technologies at
http://webtide.intalio.com/2011/09/cometd-2-4-0-websocket-benchmarks/
found an over 150x factor in favor of WebSockets (700ms vs. 3 ms at 50,000 users).

## <a name="PerftestScripts"> Performance Testing Script</a>
QUESTION:
Can Visual Studio do it?


## <a name="References"> References</a>
 * HTML5 Web Sockets - http://social.technet.microsoft.com/wiki/contents/articles/7148.websockets-in-asp-net.aspx
