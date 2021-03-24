# NLog.Targets.Gelf
NLog.Targets.Gelf is an [NLog] target implementation to push log messages to [GrayLog2]. It implements the [Gelf] specification and communicates with GrayLog server via UDP.

## History
Code forked from https://github.com/ARSFI/NLog.Targets.Gelf

### Configuration
Here is a sample nlog configuration snippet:
```xml
<configSections>
  <section name="nlog" type="NLog.Config.ConfigSectionHandler, NLog" />
</configSections>

<nlog xmlns="http://www.nlog-project.org/schemas/NLog.xsd"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

	<extensions>
	  <add assembly="NLog.Targets.Gelf"/>
	</extensions>

	<targets>
	  <!-- Other targets (e.g. console) -->
	
	  <target name="gelf" 
			  xsi:type="gelf" 
			  endpoint="udp://logs.local:12201"
			  facility="console-runner"
			  sendLastFormatParameter="true"
	  >
		<!-- Optional parameters -->
		<parameter name="param1" layout="${longdate}"/>
		<parameter name="param2" layout="${callsite}"/>
	  </target>
	</targets>

	<rules>
	  <logger name="*" minlevel="Debug" writeTo="gelf" />
	</rules>

</nlog>
```

Options are the following:
* __name:__ arbitrary name given to the target
* __xsi:type:__ set this to "gelf"
* __endpoint:__ the uri pointing to the graylog2 input in the format udp://{IP or host name}:{port} *__note:__ support is currently only for udp transport protocol*
* __facility:__ The graylog2 facility to send log messages
* __sendLastFormatParameter:__ default false. If true last parameter of message format will be sent to graylog as separate field per property

