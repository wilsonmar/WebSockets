This page introduces you to JMeter in a deeply technical hands-on way working on full samples, not incomplete demos.
Rather than bombarding you with random concepts and making obvious statements,
concepts are pointed out along the way at "teachable moments".
PROTIP of "best practices" are noted when appropriate, as are
Similarities to LoadRunner, Visual Studio, and other similar tools.

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
0. <a href="#Download4PC"> Download JMeter for PCs</a>
0. <a href="#Download4Mac"> Download JMeter for Macs</a>
0. <a href="#Plugins"> JMeter Plug-ins</a>
0. <a href="#InvokeUI"> Invoke JMeter UI</a>
0. <a href="#TestPlanFolders"> Test Assets Folders</a>
0. <a href="#GetSampleTest"> Get Sample Test Assets from Github</a>
0. <a href="#SetupServerUnderTest"> Setup Python Server Under Test</a>
0. <a href="#ExamineAppCode"> Examine Sample App Code</a>
0. <a href="#ExamineSampleTest"> Examine Sample Test Plan Assets</a>
0. <a href="#PythonSetup"> Setup for Python</a>
0. <a href="#JMeterUI"> JMeter UI Run</a>
0. <a href="#RunBatch"> Run in Batch Mode</a>
0. <a href="#ViewLog"> View Log File</a>
0. <a href="#ViewResultTree"> View Result Tree</a>
0. <a href="#NewTestPlan"> New Test Plan</a>
0. <a href="#ThreadGroups"> Thread Groups</a>
0. <a href="#Workbench"> Workbench</a>
0. <a href="#TestPlan"> Test Plan Elements</a>
0. <a href="#Samplers"> Samplers</a>
0. <a href="#ConfigNodes"> Configuration Nodes</a>
0. <a href="#LogicControllers"> Logic Controllers</a>
0. <a href="#Timers"> Timers</a> (to add delays)
0. <a href="#PreProcessors"> Pre-Processors</a>
0. <a href="#PostProcessors"> Post-Processors</a>
0. <a href="#Listeners"> Listeners</a> (for reporting, logging, debugging)
0. <a href="#Attributes"> Attributes</a>
0. <a href="#Assertions"> Assertions</a> (for error checking)
0. <a href="#SimulateJavaScript"> Simulate JavaScript</a>
0. <a href="#SetupThreadGroup"> Setup Thread Group</a>
0. <a href="#tearDownThreadGroup"> tearDown Thread Group</a>


## <a name="Java"> Java SDK Pre-requisite</a>
JMeter was written in Java from
http://www.oracle.com/technetwork/java/javase/downloads/index.html

The path to the Java bin folder must be in the system PATH environment variable
so Java executables can be found. See https://wiki.apache.org/jmeter/TestRecording210

The path to JVM_HOME also needs to be defined, such as 
set JAVA_HOME=C:\jdk1.7.0_45

This is the same across operating systems, which is why JMeter can run on PC and Mac.


## <a name="Download4PC"> Download, Install JMeter for PCs</a>
PROTIP:
Instead of following what <a target="_blank" href="http://zacster.blogspot.com/2008/03/quick-howto-to-setup-jmeter.html">
Zac explained in 2008</a> and download from a mirror website on the
<a target="_blank" href="http://jmeter.apache.org/download_jmeter.cgi"> 
Apache download web page</a>,
you then need to unzip, create a folder, move it, etc.
I think it's simpler to:

1) If you haven't already, open an internet browser,
  go to https://chocolatey.org/ and copy the whole @powershell command.
  Open a command window and paste the command to install Chocolatey.
  Exit the command.

2) Open a command window to run this command (described at https://chocolatey.org/packages?q=jmeter).
  (Instead of `choco install jmeter -y`).

```
inst jmeter -y
```

Chocolatey installs without prompting for more user interaction.
So it's useful in server automation scripts.

NOTE: Instructions below are based on version 2.1.2 downloaded June 30, 2015.


## <a name="Download4Mac"> Download, Install JMeter for Macs</a>
Similarly, on the Mac, open a Terminal windows and use Homebrew:

```
brew update
brew install jmeter --with-plugins
```

These instructions update instructions
<a target="_blank" href="http://biscminds.blogspot.fr/2011/12/quick-jmeter-setup-on-mac.html">
here from 2011</a> when JMeter was still under the Apache Jakarta project.

http://www.apache.org/info/verification.html

JMETER_BIN ???

Since <storng>apache-jmeter-2.12.zip</strong> was installed,
Homebrew saves jmeter to folder <strong>/usr/local/Cellar/jmeter/2.12/libexec</strong>.
This is good to know for adding plug-ins, whose
<strong>jar</strong> files go into JMeter's <strong>lib/ext</strong> (extension) folder.

Jar files contents should follow
http://maven.apache.org/guides/introduction/introduction-to-the-standard-directory-layout.html

The <strong>pom.xml</strong> file in a github repository is used by maven to create jar files,
perhaps with a script such as:
https://draptik.wordpress.com/tag/pom-xml/

See https://ribblescode.wordpress.com/2012/04/16/how-to-run-jmeter-tests-with-maven/

Create the jar file using Maven ???

http://jmeter.lazerycode.com/


## <a name="Plugins"> JMeter Plug-ins</a>
Plug-ins extend the capability of JMeter.

In Eclipse IDE, export it to a JAR.

Samplers plug-in for WebSockets:

  * https://github.com/kawasima/jmeter-websocket was last updated by Yoshitaka Kawashima in 2013.

    The path `src/main/java/net/unit8/jmeter/protocol/websocket/control/gui` contains
    
      * WebSocketSamplerGui.java

    The path `src/main/java/net/unit8/jmeter/protocol/websocket/sampler` contains

      *  WebSocketSampler.java

    The path `src/main/resources/net/unit8/jmeter/protocol/websocket/sampler` contains 
    
      * WebSocketSamplerResources_ja.properties (Japanese translation overrides)
      * WebSocketSamplerResources.properties

    The path `src/test/java/net/unit8/jmeter/protocol/websocket/sampler` contains
    
      * WebSocketSamplerTest.java

    The path `src/test/resources` contains
    
      * jmeter.properties
      * saveservice.properties
      * users.csv

    The path `src/test/scripts` contains
    
      * chat.js

  * https://github.com/maciejzaleski/JMeter-WebSocketSampler was last updated by Maciej Zaleski in 2013.
  
    It features a Swing GUI. 
  
    The path `src/main/java/JMeter` contains a controler [sic] folder and functional folder.
    The path `src/main/java/JMeter/plugins/functional/samplers` contains java program code:

      * ServiceSocket.java
      * WebSocketImplementation.java
      * WebSocketSampler.java
      * WebSocketSamplerGui.java
      * WebSocketSamplerPanel.form
      * WebSocketSamplerPanel.java

    The path `src/main/java/JMeter/plugins/controler`

      * WebSocketApplicationConfig.form
      * WebSocketApplicationConfig.java
      * WebSocketApplicationRequest.form
      * WebSocketApplicationRequest.java
      * WebSocketApplicationResponse.form
      * WebSocketApplicationResponse.java
      * WebSocketSampler.java
      * WebSocketSamplerGui.java

Others:

* https://github.com/undera/jmeter-plugins (described in http://jmeter-plugins.org/wiki/PluginInstall/)
  are shown in menus prefixed with "jp@gc".

* https://github.com/ATLANTBH/jmeter-components.
  provides samplers for JSON, OAuth, HBase and Hadoop, etc.

* https://github.com/afranken/jmeter-analysis-maven-plugin
is a Maven plugin that parses JMeter result XML files and generates detailed reports with charts
Can be used in combination with the JMeter Maven Plugin 
https://github.com/afranken/jmeter-analysis-maven-plugin
developed by the same author.

* http://stackoverflow.com/users/460802/ubik-load-pack

* https://github.com/flood-io/ruby-jmeter
  is a Ruby based DSL (Domain Specific Language) for building JMeter test plans 

* https://github.com/flood-io/ruby-jmeter 
is the most forked among jmeter repos. It is used to work with the flood.io cloud testing service.


## <a name="GetSampleTest"> Get Sample Test Assets from Github</a>
Unlike other tutorials that only scratches the surface,
let's look at a JMeter test plan that has scripting logic often needed.

1) Open an internet browser to https://github.com/wilsonmar/99bottles-jmeter
  which was forked from https://github.com/groodt/99bottles-jmeter (dated November, 2011 and not updated since).

2) Click <strong>Download ZIP</strong> to obtain file name ending with <strong>-master.zip</strong>
  then unzip. 
  Or use git to clone the repo locally.

3) Copy the repo's path to the Clipboard.

  On a Mac Finder window opened to the repo stored locally, 
  right-click on <strong>requirements.txt</strong> 
  and select Get Info. Double-click on "99bottles" within the Where: text
  until the whole path is highlighted.
  Press command+C to store the highlighted string in the Clipboard.

4) Open a command or Terminal window.

5) Type `cd` and paste the Clipboard containing the path to the "99bottles" repo folder on your local drive.
  For example:
  
```
  /Users/wilsonmar/Downloads/99bottles-jmeter-master
```

6) View files by typing `ls` then Enter. The response:

```
README.md        jmeter.log       
Test Plan.jmx    requirements.txt server.py
```

## <a name="SetupServerUnderTest"> Setup Python Server Under Test</a>
The env1 folder contains a <strong>server.py</strong> Python script.
So the Python package installer (pip) needs to be installed.

1) Install pip. On PCs see http://tylerbutler.com/2012/05/how-to-install-python-pip-and-virtualenv-on-windows-with-powershell/
  which makes use of a Powershell clone of the unix scripts.
  On Macs:

```
sudo easy_install pip
```

2) Create a virtualenv for Python. 
  (as described in the "99 Bottles of JMeter on the wall" website
  http://tech.mindcandy.com/2011/11/99-bottles-of-jmeter-on-the-wall )

```
pip install virtualenv
```

3) Use virtualenv to install virtualenvwrapper:
  (based on http://virtualenvwrapper.readthedocs.org/en/latest/)

```
sudo pip install virtualenvwrapper
```

4) Create environment variable $WORKON_HOME. On PCs, it's at `c:\python27\lib\site-packages`
On Macs:

```
export WORKON_HOME=~/Envs
mkdir -p $WORKON_HOME
echo $WORKON_HOME
ls $WORKON_HOME
source /usr/local/bin/virtualenvwrapper.sh
```

5) Make custom virtual environment:

```
cd to where your 99bottles is installed
mkvirtualenv env1
mkvirtualenv 99bottles --no-site-packages
```

The response:

```
  New python executable in 99bottles/bin/python
  Installing setuptools, pip...done.
  (env1)
```

6) Install dependencies:

```
cd 99bottles-jmeter
pip install --requirement=requirements.txt
```

7) Invoke server:

```
./server.py
```

The response:

```
  Bottle server starting up (using PasteServer())...
  Listening on http://localhost:9999/
  Use Ctrl-C to quit.
  
  serving on http://127.0.0.1:9999
```

Stopping the command/terminal window stops the app server.


## <a name="ExamineAppCode"> Examine Sample App Code</a>
7) Open in a text editor utility the <strong>server.py</strong> application code.
  The print() function outputs should look like this:

```
25 bottles of mead on the wall. Date=1436066062941 Thread=0
127.0.0.1 - - [04/Jul/2015:21:14:22 -0600] "POST /bottle HTTP/1.1" 200 7 "-" "Apache-HttpClient/4.2.6 (java 1.5)"
```

In this example, the date 1436066062941 is a Unix Epoch of seconds since Jan. 1, 1970.


## <a name="ExamineSampleTest"> Examine Sample Test Plan Assets</a>
General Variables (key value pairs) defined are available for use within JMeter configuration elements.

In Thread Group, ${threads} and ${loopCount}. (Loop count is equivalent to what LoadRunner calls iterations)

The Loop Controller has a loop count of 1 (once). 

Under that is a HTTP Request element that uses variables to specify the URL:

```
http://${host}:${port}/bottle
```

Variables are also used in the request body spec:

```
{"drink":"${drink}", "bottles":"${bottles}", "date":"${date}", "thread":"${thread}"}
```

The <strong>BSF PreProcessor</strong> executes <strong>JavaScript</strong> and other programming languages.

PROTIP: 
https://blazemeter.com/blog/beanshell-vs-jsr223-vs-java-jmeter-scripting-its-performance
reports that native compiled Java runs twice faster than JSR233/Groovy and BeanShell scripts.



## <a name="InvokeUI"> Invoke JMeter UI</a>
1) Open a new command or terminal window.

2) Invoke the JMeter UI by typing in `Jmeter`.

  On the PC this invokes <strong>Jmeter.bat</strong>.

  Wait for the JMeter window to appear.

  WARNING: Do not dismiss the command/terminal window which invoked JMeter.

3) Press command + N or click menu <strong>File | Open</strong>.

  On a Mac, notice the default location of test plans is <strong>usr</strong>.
  
  Notice the file format is JMeter [<strong>.jmx</strong>].
  
4) Select menu Open.

5) Navigate to the test plan file described above: `/Users/wilsonmar/Downloads/99bottles-jmeter-master`

6) Make sure menu <strong>Options | Log Viewer</strong> is checked so logs appear in the lower-right pane.

7) To see more log entries, click on the edge above the log pane.
   Scroll to the far left of log entries.
   
8) Run the test from the JMeter UI one of several ways:

  * Click the Run button
  * Select menu Run | Start
  * Press command + R.

9) During the run, at the upper-right corner in the gray bar is "0/1".


## <a name="ViewResultTree"> View Result Tree</a>
1) This was created by right-clicking Thread Group, then Listeners, View Result Tree element.

  This captures details on each request and response.
  
  QUESTION: Can JMeter capture in a buffer and not display unless there is an error, like what LoadRunner does?

2) Click on an exchange, typically "HTTP Request".

3) Click on Request.

  This details the URL end-point, such as `http://localhost:9999/bottle`
  and the JSON-formatted POST data, which you can toggle between Raw and HTTP.
  
  `Content-Type: application/json` means that 
  JSON data is expected back.

4) Click on Sampler result.

  The expected response header is `HTTP/1.0 200 OK`.

5) Click on Response Data.

  "Cheers!" is what the server.py program returns.

NOTE: This detail for every request/response exchange is expensive to capture and store.


## <a name="RunBatch"> Run in Batch Mode</a>
JMeter is often invoked automatically by a continuous integration tool such as Jenkins.
See https://wiki.jenkins-ci.org/display/JENKINS/Performance+Plugin.

1) Open a command (terminal) window.

2) Type cd and paste the file path to the test plan.

3) Type:

```
jmeter -n -t "Test Plan.jmx" -l run001.jtl
```

* Parameter `-n` specifies no GUI.
* Parameter `-t "Test Plan.jmx"` specifies the test plan.
* Parameter `-l run001.jtl` specifies the text file to hold results from the run. See http://wiki.apache.org/jmeter/JtlFiles.
* Parameter `-p parameters.txt` specifies the parameters to define.

PROTIP:
Avoid using spaces in test plan names.

Example response to the Terminal:

```
Creating summariser <summary>
Created the tree successfully using Test Plan.jmx
Starting the test @ Sat Jul 04 06:45:16 MDT 2015 (1436013916367)
Waiting for possible shutdown message on port 4445
summary +    876 in  14.3s =   61.4/s Avg:   129 Min:     0 Max:  2011 Err:   876 (100.00%) Active: 10 Started: 10 Finished: 0
summary +    124 in   2.1s =   58.4/s Avg:   146 Min:     0 Max:  2005 Err:   124 (100.00%) Active: 0 Started: 10 Finished: 10
summary =   1000 in  14.4s =   69.5/s Avg:   131 Min:     0 Max:  2011 Err:  1000 (100.00%)
Tidying up ...    @ Sat Jul 04 06:45:31 MDT 2015 (1436013931672)
... end of run
(env1)
```

## <a name="ViewLog"> View Log File</a>

4) View the list of files with file sizes:

```
ls -all
```

In this example, the output file as 211,148 bytes:

```
  -rw-r--r--    1 wilsonmar  staff  211148 Jul  4 06:45 run001.jtl
```

5) Open the file using a text editor:

```
1436013917275,67,HTTP Request,Non HTTP response code: org.apache.http.conn.Http$
```


## <a name="Languages"> Languages</a>
Python is one of several programming languages that JMeter can support.


## <a name="NewTestPlan"> New Test Plan</a>
We next create a new test.


## <a name="ThreadGroups"> Thread Groups</a>
Load on servers is imposed by activities within various program <strong>thread</strong>.
The more threads, the more virtual users are being simulated.

1) Create the <strong>Thread Group</strong> for the Test Plan: 
Right-Click on Test Plan to select <strong>Edit | Add</strong> to create a <strong>Thread Group</strong>.

  NOTE: Thread groups define the metadata

2) In the current situation (for recording described below), use 1 user and loop count 1.

3) PROTIP: Change the Thread Group's name to summarize the various settings, 
   such as "1UserRecorded".

4) Depending on the type of test, change the <strong>Ramp-up period</strong> 
   to provide one second per user. For example, for 2 users, specify 2 seconds.
   For now, leave the default of 1.

Add directory to jar or classpath


## <a name="Workbench"> Workbench</a>
WorkBench is a temporary space to store a test plan's elements,
such as requests recorded (captured) by a proxy and converted into commands.

Below is a remix of
https://chipcorrera.wordpress.com/2010/01/25/using-jmeter-and-firefox-to-load-test/
by Chip Correra and
http://jmeter.apache.org/usermanual/jmeter_proxy_step_by_step.pdf


1) Get Firefox to use the JMeter proxy ???

Now, lets set up Firefox to proxy actions. Bring up the Firefox browser and 
  under Tools/options/advanced tab/network tab/settings button/”Manual proxy configuration”
  + Set 127.0.0.1 port 9090
  + Enable the “Use this proxy for all protocols” check box.


2) Configure Internet Options to define Manual proxy configuration to localhost port 8080.

3) Right-click on Workbench to Add | <strong>Non-test Elements | HTTP(S) Test Script Recorder</strong>.

4) Right-click on Recorder to Add | <strong>Logic Controller | Recording Controller</strong>
    (Once Only Controller)
    If your application has a user login which generates session cookies,
    otherwise skip this step and the next.

  This conveniently packages all samples under one controller, which can be given a name that describes the test case.

5) Right-clock Thread Group to Add | Config Element | HTTP Request Defaults.
  This applies to your entire test suite.

6) Specify <strong>Server Name or IP</strong> address and any required port #.

  Other tutorials use google.com or jmeter.apache.org.
  One live demo WebSockets website is 

7) Add a HTTP Cookie Manager config element
    This can be used to control and manage the cookie policy across the test.

8) Add a HTTP Request Sampler to the Once Only Controller
    Specify the protocol method (put/get), path to the request and any parameters

9) Test Plan > Add > Listener > Aggregate Report.

11) Right-click Workbench to Add | Non-Test Element | HTTP Proxy Server
  + Port 9090
  + Target Controller: Thread Group > Recording Controller
  + Patterns to include: Click Add then enter “.*”

12) Under HTTP Proxy Server, Add > Timer > Gaussian Random Timer
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



## <a name="Samplers"> Samplers</a>
JMeter <strong>samplers</strong> emulate real clients by sending (a lot of) requests to servers.



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


## <a name="Timers"> Timers</a>
The time period to wait between requests are defined by <strong>timers</strong>,
also known as "think time" in LoadRunner.
By default, requests are executed immediately one after another without any waiting time.


## <a name="PreProcessors"> Pre-Processors</a>
Before a sampler is executed, elements (actions, assertions or basically whatever) that is going to happen 
are defined in <strong>pre-processors</strong> which
extract variables from a response that can be used in the sampler afterwards via configuration elements.

Pre-processor is able to create variables for the next steps (sampler or any other entity in current thread group), something like vars.put("variable_name", "variable_value") in the pre-processor followed by ${variable_name} wherever you need to refer it. 

## <a name="BSFPreProcessors"> BSF Pre-Processors</a>

  BSF is the Bean Scriptingl Framework at http://beanshell.org/manual/bsf.html
  and http://commons.apache.org/proper/commons-bsf/
  and https://en.wikipedia.org/wiki/Bean_Scripting_Framework
  
 It is generic framework that allows many scripting languages to be plugged into an application. It shields the application from knowledge of how to invoke the scripting languages and their APIs, via adapter "engines". 
  BeanShell dynamically executes Java code (is a Lightweight embedded Java source interpreter that).
  for Java per [JSR223](http://jcp.org/en/jsr/detail?id=274)
  described on http://www.drdobbs.com/jvm/jsr-223-scripting-for-the-java-platform/215801163
  
  BSP supports dynamic execution of JavaScript, achieved using Mozilla Rhino engine (from 
  https://developer.mozilla.org/en-US/docs/Mozilla/Projects/Rhino)
  which is also used in Oracle JVM.
 
 However, it is recommended that for "heavy" operations it's better to use JSR223 Sampler and Groovy as a language.
 See https://blazemeter.com/blog/beanshell-vs-jsr223-vs-java-jmeter-scripting-its-performance
 
  It uses the ScriptEngine interface which became available in Java 6.
 
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



## <a name="SetupThreadGroup"> Setup Thread Group</a>
If there is work to do just once before iterating through,
  select menu <strong>Edit | Add</strong> to create a <strong>setUp Thread Group</strong>.
  This is similar to the LoadRunner VuserInit action.

## <a name="tearDownThreadGroup"> tearDown Thread Group</a>
Create a <strong>tearDown Thread Group</strong> to execute once.
This is similar to the LoadRunner VuserEnd action.


## Others
Start no pauses.

Maven build tool which manages dependencies.

https://github.com/oliverlloyd/jmeter-ec2
Automates running Apache JMeter on Amazon EC2 


QUESTION: Who is working on JMeter's use of "Nashon" Groovy and Ruby engine in Java 8.
Its REPL (Read, Eval, Print Loop) shell (jjs> prompt) interactively inteprets JavaScript inside Java programs.

http://janalyser.com/
