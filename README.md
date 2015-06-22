This mark-down text page and associated solution files demonstrates how to program and performance test
HTTP5 WebSockets implemented in the C# language within Visual Studio 
using Microsoft's SignalR library on the server and various client technologies.

Applications such as stock and sports tickers, on-line gaming, inventory trackers, 
chats, and other apps needing "real-time" updates 
without the need for users to manually refresh the screen or click a button. 

SignalR 2 comes with Visual Studio 2013.
https://www.youtube.com/watch?v=QL-HPsC1SH0


### <a name="ObserveRealTimeTech"> Observe Older Real-Time Technologies</a>
1). Open a browser which does not support WebSockets, such as Internet Explorer 9.
(this may involve using a VMWare instance)

2). Press F12 or right-click and select **Inspect Element** 
 to Trace the HTTP packets involved.

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


The RTMP (Real Time Message Protocol) was used within Adobe Flash since 2003,
but it's proprietary.


### <a name="JavaFirst"> Java Origins</a>
Because the JSR-356 deliver a Java API in Java EE 7,
the first implementations of WebSockets were in the Java language.

<a href="http://lightstreamer.com/"> LightStreamer</a>
is a commercial product (with a Java open-source free version)
that provides so many more sophisticated features that make other implementations seem like "toys". 

There is a commercial product (with an open-source free version)
that provides so many more sophisticated features that make other implementations seem like "toys". 

It is programmed in Java.

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


PHP programs can support WebSockets using http://socketo.me/


### <a name="DemoApps"> Demo Apps</a>
1). Open a modern browser 

http://caniuse.com/#search=websockets
shows can almost all browsers in 2015 supports WebSockets.

2). Press F12 to Trace the HTTP packets involved.

3). Specify the URL of one of these demo sites created using WebSockets technology:

 <a target="_blank" href="https://jabbr.net/">
 <img align="right" src="https://cloud.githubusercontent.com/assets/300046/8271426/6edde23a-17d4-11e5-9949-6bffe160d06d.png" 
 /></a>
 * <a target="_blank" href="https://jabbr.net/">https://jabbr.net</a>
  is a browser chat web app written using <a href="#SignalR"> Microsoft ASP.NET SignalR</a>
  and featured at the upper-right corner on asp.net web page.

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

The first version of the framework which supports SignalR is **4.5**.

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

### <a name="RealTimeTech"> Older Real-Time Technologies</a>
Before WebSockets, programmers "hacked" ways 
Web sockets techonology is also used for communication between two servers without a human UI.

Newer WebSockets technologies **fall back** to these in this sequence of preference:

   1. Server Sent Event (SSE) - part of HTML5/W3C (Event Source)
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


### <a name="HTTPProxies"> HTTP Proxies</a>
Some organizations use transparent HTTP Proxy servers to filter all network traffic
to monitor conditions for security by shutting off connections that are open too long.

HTTP proxies were designed for HTTP document transfer and not for long-lived connections

HTTP Proxies may not be configured to propogate UPGRADE headers.



### <a name="NodeJS"> NodeJS Implementations</a>
The Socket.io module for Node.js


### <a name="SignalR"> Microsoft Web Sockets SignalR</a>
To implement Web Sockets Microsoft offers its SignalR library 
described at http://SignalR.net and stored as open-source repo at
http://github.com/Microsoft/SignalR
by 
Damien Edwards, SignalR developer. 

https://www.youtube.com/watch?v=us-Q3do-N7M
TechNet North America
SignalR: Building Real-Time Applications with ASP.NET SignalR [59:44] May 19 2014
by Brady Gaster building a HitCounter using Ultimate 2013.


https://www.youtube.com/watch?v=0nMAuigjYh8
Lunch & Learn - Real Time Web Messaging with SignalR
by LogicalAdvantage

https://www.youtube.com/watch?v=WJpoDCGEIW0
by Chris Johnson

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

A **hub** is a high-level **pipeline** built upon the Connection API 
that allows client and server to call methods on each other directly.



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

<a target="_blank" href="https://cloud.githubusercontent.com/assets/300046/8271005/37c9aa02-17bd-11e5-8644-c105418811f9.png">
<img align="right" src="https://cloud.githubusercontent.com/assets/300046/8271005/37c9aa02-17bd-11e5-8644-c105418811f9.png"
width="200" /></a>
6). Instead of the default `public void Hello()`

```
 public void SendMessage(string message){
     Clients.All.hello();
 }
```

The default hello method of the Clients class sends a string to All clients connected.

A more realistic/common in the protocol response dynamically injects paramater values:

```
 var msg = string.Format ("{0}: {1}", Context.ConnectionId, message);
 Clients.All.newMessage( msg );
```

 
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

## Grouping (by Chat Room)
Connections and messages can be grouped into a collection such as a Room.

```
public void JoinRoom(string room) {
    Groups.Add( Context.ConnectionId, room );
}
public void SendMessageForRoom( string room, string message) {
    var msg = string.Format("{0}: {1}", Context.ConnectionId, message );
    Clients.Group(room).newMessage(msg);
}
```

SignalR2 makes use of groups to differentiate anonymous connections by users who have not been authenticated.
See https://www.youtube.com/watch?v=QL-HPsC1SH0.

https://www.youtube.com/watch?v=QL-HPsC1SH0&t=4m24s
SignalR2 introduces the **HubException** error type used in a CauseError method.

On the client-side JavaScript:

```
$("#causeError").click(function (){
    hub.server.causeError(-1)
        .fail(functrion(err) {
            $("#errorMessage").text(err.message);
        });
});
```

The "source" property ???

SignalR dos not automatically persist groups on the server.
Thus group counts are not provided by default.


## <a name="WSS"> WSS</a>
Instead of HTTP or HTTPS, WebSockets use the WSS protocol.

## <a name="OfflineMode"> Offline Mode</a>
QUESTION: How does WebSockets handle connections that fade out.

Are messages buffered in the client and server side?

QUESTION: Keep-alive pings and heartbeats to make sure browsers don't time out (after default 2 minutes)
are not built into the WebSockets protocol.

## Scraps

serialized into and deserialized from JSON (using the JSON.NET library).

Like other ASP.NET (such as MVC), first define a **route** in the host process definition code.
???

## <a name="LifeCycle"> Lifecycle</a>
QUESTION: Override pipeline event handlers or retrieve hub context via dependency resolver.

## <a name="OnConnected"> OnConnected</a>
Upon connection (such as opening a new browser window) ...

## <a name="OnDisconnected"> OnDisconnected</a>
Upon disconnection (such as closing of a browser window) ....

## <a name="OnReconnected"> OnReconnected</a>



## <a name="OWinStartup"> OWin Startup Routing</a>
SignalR2 specifies the StartUp class:

```
Using Microsoft.Owin;
using Owin;
using MyWebApplication;

[assembly: OwinStartupAttribute(typeof(WebApplication100.Startup))]
namespace WebApplication100 {
    public partial class Startup {
        public void Configuration(IAppBuilder app) {
            ConfigureAuth(app);
            app.MapSignalR();
        }
    }
}
```

**Startup.cs** needs to be added to call app.MapSignalR() within Configuration
to de-couple use of IIS System.Web controlled by global.aspx. 

Like routing. ???

Starting in OWin enables **self-hosting** outside ASP.NET (System.Web).

ConfigureAuth(app); is added ???



## <a name="AddHTML"> Default.HTML Page</a>

Drag from Solution Manager:

```
<script src="Scripts/jquery-1.6.4.js"></script>
<script src="Scripts/jquery.signalR-2.0.3.js"></script>
<script type="text/javascript">
```

Create a physical connection (con)
to which the "hub" acts as a proxy object to text handling code.

```
    $(function(){
        var con = $.hubConnection();
        var hub = con.createHubProxy('hitCounter');
        hub.on('onHitRecorded', function(i) {
            $('#hitCount').text(i);
        });
        con.start( function(){
            hub.invoke('recordHit');
        });
    })
</script>
```



## <a name="Hub.cs"> Hub.cs</a>
Right-click HitCounter to Add | SignalR Hub Class (v2) | named "HitCounterHub.cs"

Add the app name:

```
[HubName("hitCounter")]
```

Initialize the counter:

```
private static int _hitCount = 0;
```

Increment the counter:

```
    _hitCount += 1;
```

Accounce the counter:

```
    this.Clients.All.onHitRecorded(_hitCount);
```
## <a name="UnreliableConnection"> Unreliable Connection</a>
Assume that about 1 out of 100 messages are dropped.


## <a name="BenchmarkStudies"> Benchmark Studies of Efficiency and Scalability</a>
Comparison of Comet vs. WebSockets technologies at
http://webtide.intalio.com/2011/09/cometd-2-4-0-websocket-benchmarks/
found an over 150x factor in favor of WebSockets (700ms vs. 3 ms at 50,000 users).

## <a name="Scaling Out"> Scaling Out</a>
A **backplane** allows apps to scale to multiple servers
by receiving messages and forwarding them to other app instances.

http://www.asp.net/signalr/overview/guide-to-the-api/handling-connection-lifetime-events
from June 10, 2014.

## <a name="PerftestScripts"> Performance Testing Script</a>
QUESTION:
Can Visual Studio do it?


## <a name="References"> References</a>
 * https://www.youtube.com/watch?v=kyFBgephmpQ
   Real-Time Web Apps with Asp.Net SignalR
   by CodeGeek
   JonGalloway and 
   BradyGaster.com

 * HTML5 Web Sockets - http://social.technet.microsoft.com/wiki/contents/articles/7148.websockets-in-asp-net.aspx
