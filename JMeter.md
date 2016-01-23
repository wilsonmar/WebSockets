This page contains notes about use of JMeter for load testing WebSockets,
in a deeply technical hands-on way working on full samples, not incomplete demos.
Rather than bombarding you with random concepts and making obvious statements,
concepts are pointed out along the way at "teachable moments".
PROTIP of "best practices" are noted when appropriate, as are
Similarities to LoadRunner, Visual Studio, and other similar tools.

This page is based on several sources:
* https://blazemeter.com/blog/websocket-testing-apache-jmeter

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

