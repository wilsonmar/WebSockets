
This page is based on several sources:
* https://blazemeter.com/blog/websocket-testing-apache-jmeter

Download the JMeter UI installer.

Several tests can run JMeter.

Open the JMeter UI.

<a name="TestPlan"></a>
Open a Test Plan group to be executed.

A test plan can contain other test plans, to group tests by functional or technical logic together.

Each test plan can be selectively disabled for execution.

Within each <strong>test plan</strong> are these elements:

0. <a href="#Samplers"> Samplers</a>
1. <a href="#Node"> Configuration nodes</a>
2. <a href="#Preprocessors"> Pre-processors</a>
3. <a href="#Timers">Timers</a>

  If results are available: 

5. <a href="#PreProcessors"> Post processors</a>
6. <a href="#Assertions"> Assertions</a>
7. <a href="#Listeners"> Listeners</a>




<a name="Samplers"></a>
JMeter <strong>samplers</strong> emulate real clients by sending (a lot of) requests to servers.
One sampler for WebSockets was created by 
https://github.com/maciejzaleski/JMeter-WebSocketSampler

<a name="ThreadGroups"></a>
Samplers run as <strong>Thread groups</strong>.
The more threads, the more virtual users are being simulated.

Each group contains <strong>nodes</strong> which contain various <strong>elements</strong>.

<a name="Nodes"></a>
Nodes are associated with 
different parameters passed into sampler request code by using 
<strong>configuration elements</strong> which provide values to
<strong>variables</strong> referenced by sampler code.

<a name="LogicControllers"></a>
The order of execution of different samplers is controlled by
<strong>Logic controllers</strong>: 
If, While, FoEach, Loop, Random, etc.


<a name="PreProcessors"></a>
Before a sampler is executed, elements (actions, assertions or basically whatever) that is going to happen 
are defined in <strong>pre-processors</strong> which
extract variables from a response that can be used in the sampler afterwards via configuration elements.

<a name="Timers"></a>
The time period to wait between requests are defined by <strong>timers</strong>,
also known as "think time" in LoadRunner.
By default, requests are executed immediately one after another without any waiting time.


<a name="PostProcessors"></a>
After a sampler execution finishes,
response data from the server can be parsed to extract values 
by <strong>post-processors</strong>.


<a name="Listeners"></a>
Output from samplers to tables, trees, or plain log files are formatted by
<strong>listeners</strong>
provide different ways to view the results produced by a Sampler requests. 

<a name="Attributes"></a>
In the various listeners,
sample results have various attributes (success/fail, elapsed time, data size etc).


<a name="Assertions"></a>
Validation of the validity of what was returned from the server is done by 
<strong>assertions</strong>, which are based on the format of the response:
HTTP, XML, JSON, etc.


## <a name="Run"> Run</a>
A test is invoked several ways:

* Click the Run button
* Select menu Run | Start
* Press command + R.

Start no pauses.



