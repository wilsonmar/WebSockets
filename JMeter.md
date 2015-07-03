This page introduces you to JMeter in a hands-on way, with concepts pointed out along the way.
(rather than bombarding you with random concepts)
Similarities to LoadRunner, Visual Studio, and other similar tools is pointed out along the way.
PROTIP of "best practices" are noted when appropriate.

This page is based on several sources:
* https://blazemeter.com/blog/websocket-testing-apache-jmeter
* http://www.javacodegeeks.com/2014/11/jmeter-tutorial-load-testing.html
* https://www.youtube.com/watch?t=933&v=8D6nKml88vE by Ashish Takur, who also published paid content at
* http://loadrunnerjmeter.com
* http://www.pluralsight.com/courses/java-web-fundamentals by Kevin Jones about creating Java servlets,
  filters (controllers), and listeners. These are build using IntelliJ, built using Maven,
  and run on Tomcat.apache.org web servers.
* https://www.youtube.com/watch?v=4mfFSrxpl0Y JMeter Load Testing Beginner Tutorial
* https://www.youtube.com/watch?v=cv7KqxaLZd8 Learn JMeter in 60 minutes by Ophir of BlazeMeter

## Contents
0. <a href="#Java"> Java SDK Pre-requisite</a>
0. <a href="#Download"> Download</a>
0. <a href="#TestPlanFolders"> Test Assets Folders</a>
0. <a href="#SampleTestPlans"> Sample Test Plans</a>
0. <a href="#RunBatch"> Run in Batch Mode</a>
0. <a href="#JMeterUI"> JMeter UI Run</a>
0. <a href="#ThreadGroups"> Thread Groups</a>
0. <a href="#Workbench"> Workbench</a>
0. <a href="#TestPlan"> Test Plan Elements</a>
0. <a href="#Samplers"> Samplers</a>
0. <a href="#ConfigNodes"> Configuration Nodes</a>
0. <a href="#LogicControllers"> Logic Controllers</a>
0. <a href="#Timers"> Timers</a> (to add delays)
0. <a href="#Listeners"> Listeners</a> (for reporting, logging, debugging)
0. <a href="#Attributes"> Attributes</a>
0. <a href="#Assertions"> Assertions</a> (for error checking)
0. <a href="#SimulateJavaScript"> Simulate JavaScript</a>
0. <a href="#Plugins"> JMeter Plug-ins</a>


## <a name="Java"> Java SDK Pre-requisite</a>
JMeter was written in Java.

The path to the Java bin folder must be in the system PATH environment variable
so Java executables can be found.

The path to JVM_HOME also needs to be defined.

This is the same across operating systems, which is why JMeter can run on PC and Mac.


## <a name="Download"> Download JMeter</a>
If you run Windows, rather than downloading and running the installer directly from a mirror listed 
<a target="_blank" href="http://jmeter.apache.org/download_jmeter.cgi"> Apache website</a>
(as <a target="_blank" href="http://zacster.blogspot.com/2008/03/quick-howto-to-setup-jmeter.html">
Zac explained in 2008</a>),
I think it's simpler to:

1) open a command window,

2) install Chocolatey in Powershell (if your haven't already)

3) run the command (described at https://chocolatey.org/packages?q=jmeter)

```
inst jmeter -y
```

Chocolatey installs without prompting for more user interaction.
So it's useful in server automation scripts.

NOTE: Instructions below are based on version 2.1.2 downloaded June 30, 2015.


## <a name="TestPlanFolders"> Test Assets Folders</a>
1) Switch to Windows Explorer or Finder 
  (Press Ctrl+Tab or command+Tab). 

2) Create a folder to hold test assets. Test plans are containers.

3) Open an internet browser to https://github.com/jribble/jmeter-demo
(http://github.com/wilsonmar/WebSockets/JMeterSimpleDemo1).
  
4) Click <strong>Download ZIP</strong> to obtain file name ending with <strong>-master.zip</strong>.

5) Unzip.

## <a name="SampleTestPlans"> Sample Test Plans</a>

3) Copy sample scripts within the folder.


## <a name="RunBatch"> Run in Batch Mode</a>
JMeter is often invoked automatically by a continuous integration tool such as Jenkins.
See https://wiki.jenkins-ci.org/display/JENKINS/Performance+Plugin.
A sample command to invoke JMeter:

```
jmeter -n -t test.jmx -l test.jtl.
```

Parameter `-l` disables all listeners because they can be resource intensive.


## <a name="JMeterUI"> JMeter UI Run</a>
1) Invoke the JMeter UI from Windows Explorer or Mac Finder.

2) Select menu Open.

3) Navigate to the sample test plan.

Open a command window, navigate into JMeter's bin folder, and invoke <strong>Jmeter.bat</strong>.

4) Run the test from the JMeter UI one of several ways:

  * Click the Run button
  * Select menu Run | Start
  * Press command + R.

5) During the run, at the upper-right corner in the gray bar is "0/1".

6) 

## <a name="ThreadGroups"> Thread Groups</a>
Load on servers is imposed by activities within various program <strong>thread</strong>.
The more threads, the more virtual users are being simulated.

1) Create the <strong>Thread Group</strong> for the Test Plan:
  select menu <strong>Edit | Add</strong> to create a <strong>Thread Group</strong>.

2) Specify <strong>2</strong> as the initial number of Threads (users).

3) PROTIP: Change the Thread Group's name to summarize the various settings, 
   such as "2Users".

4) Depending on the type of test, change the <strong>Ramp-up period</strong> 
   to provide one second per user. For example, for 2 users, specify 2 seconds.
   
   In the current situation (for recording described below), use 1 user and loop count 1.

5) If there is work to do just once before iterating through,
  select menu <strong>Edit | Add</strong> to create a <strong>setUp Thread Group</strong>.
  This is similar to the LoadRunner VuserInit action.

6) Create a <strong>tearDown Thread Group</strong> to execute once.
This is similar to the LoadRunner VuserEnd action.

Add directory to jar or classpath


## <a name="Workbench"> Workbench</a>
WorkBench is a temporary space to store a test plan's elements,
such as requests recorded (captured) by a proxy and converted into commands.

Below is a remix of
https://chipcorrera.wordpress.com/2010/01/25/using-jmeter-and-firefox-to-load-test/
by Chip Correra


1) Get Firefox to use the JMeter proxy ???

Now, lets set up Firefox to proxy actions. Bring up the Firefox browser and 
  under Tools/options/advanced tab/network tab/settings button/”Manual proxy configuration”
  + Set 127.0.0.1 port 9090
  + Enable the “Use this proxy for all protocols” check box.


2) Configure Internet Options to define Manual proxy configuration to localhost port 8080.

3) Right-click on Workbench to Add | <strong>Non-test Elements | HTTP(S) Test Script Recorder</strong>.

2. Add a HTTP Request Defaults config element
  This can be used to specify defaults for you entire test suite.
  + Specify your Server Name or IP address and any required port #

3. Add a HTTP Cookie Manager config element
    This can be used to control and manage the cookie policy across the test.

5. Add a Once Only Controller
    My application has a user login that also generates a session cookie.
    If your application does not, you can skip this step and the next.

6. Add a HTTP Request Sampler to the Once Only Controller
    Specify the protocol method (put/get), path to the request and any parameters

7. Add a Recording Controller to the Thread Group.

8. Test Plan > Add > Listener > Aggregate Report.

9. Under Workbench, Add > Non-Test Element > HTTP Proxy Server
  + Port 9090
  + Target Controller: Thread Group > Recording Controller
  + Patterns to include: Click Add then enter “.*”

10. Under HTTP Proxy Server, Add > Timer > Gaussian Random Timer
  + Set Constant Delay Offset (in milliseconds): ${T}

And when ready to start recording the browser action just bring up the HTPP Proxy Server within JMeter and click Start. Everything that is done within Firefox will be recorded in JMeter’s recording controller. When done, just click the Stop button on the HTTP Proxy Server within JMeter.


## <a name="TestPlan"> Test Plan Elements</a>
JMeter invokes <strong>Test Plans</strong>

Test Plans are equivalent to what LoadRunner call Scenarios
which references all that is required to run a test.

Test Plans are XML files.

Open an existing Test Plan group () to be executed.

Select menu Edit | Add | Thread Group.

<a target="_blank" href="https://cloud.githubusercontent.com/assets/300046/8502621/c48a5aca-216f-11e5-860a-fb57d757bb4e.png">
<img src="https://cloud.githubusercontent.com/assets/300046/8502621/c48a5aca-216f-11e5-860a-fb57d757bb4e.png"
/></a>

To group tests by functional or technical logic together,
a test plan can contain other test plans.
Each test plan can be selectively disabled for execution.

Within each <strong>test plan</strong> are these elements:

0. <a href="#Samplers"> Samplers</a>
1. <a href="#ConfigNodes"> Configuration Nodes</a>
2. <a href="#Preprocessors"> Pre-processors</a>
3. <a href="#Timers">Timers</a>

  If results are available: 

5. <a href="#PreProcessors"> Post processors</a>
6. <a href="#Assertions"> Assertions</a>
7. <a href="#Listeners"> Listeners</a>

More samplers (for JSON, OAuth, HBase and Hadoop, etc.)
are at https://github.com/ATLANTBH/jmeter-components.


## <a name="Samplers"> Samplers</a>
JMeter <strong>samplers</strong> emulate real clients by sending (a lot of) requests to servers.

Samplers for WebSockets:

  * https://github.com/kawasima/jmeter-websocket
  * https://github.com/maciejzaleski/JMeter-WebSocketSampler


## <a name="ConfigNodes"> Configuration Nodes</a>
Nodes are associated with 
different parameters passed into sampler request code by using 
<strong>configuration elements</strong> which provide values to
<strong>variables</strong> referenced by sampler code.

Save Node as Image 


## <a name="LogicControllers"> Logic Controllers</a>
The order of execution of different samplers is controlled by
<strong>Logic controllers</strong>: 
If, While, FoEach, Loop, Random, etc.


## <a name="PreProcessors"> Pre-Processors</a>
Before a sampler is executed, elements (actions, assertions or basically whatever) that is going to happen 
are defined in <strong>pre-processors</strong> which
extract variables from a response that can be used in the sampler afterwards via configuration elements.

## <a name="Timers"> Timers</a>
The time period to wait between requests are defined by <strong>timers</strong>,
also known as "think time" in LoadRunner.
By default, requests are executed immediately one after another without any waiting time.


## <a name="PostProcessors"> Post-Processors</a>
After a sampler execution finishes,
response data from the server can be parsed to extract values 
by <strong>post-processors</strong>.


## <a name="Listeners"> Listeners</a>
Output from samplers to tables, trees, or plain log files are formatted by
<strong>listeners</strong>
provide different ways to view the results produced by a Sampler requests. 


## <a name="Attributes"> Attributes</a>
In the various listeners,
sample results have various attributes (success/fail, elapsed time, data size etc).


## <a name="Assertions"> Assertions</a>
Validation of the validity of what was returned from the server is done by 
<strong>assertions</strong>, which are based on the format of the response.

VIDEO: 
https://www.youtube.com/watch?t=74&v=kKnLsKpHn0Y (Dec. 11, 2015)
provides a 30-minute introduction to various assertions:
Duration, Size, XML, HTML, Response, XPath Compare.


## <a name="SimulateJavaScript"> Simulate JavaScript</a>
JMeter does not execute JavaScript.

If JavaScript is downloaded from the server, JMeter can only parse it for data.


## <a name="Plugins"> JMeter Plug-ins</a>
Plug-ins extend the capability of JMeter.

https://github.com/undera/jmeter-plugins


## Others
Start no pauses.

Maven build tool which manages dependencies.
