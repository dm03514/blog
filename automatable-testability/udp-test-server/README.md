# UDP Stub Server

A UDP Stub Server can be a powerful tool in automated system test arsenal.  Two popular services, statsd and syslog
both default to UDP.  Because of how critical both of these services are to an application and the critical 
visibility they provide, it can often-times be aluable to automate tests for application clients can succesfully
integrate with UDP based services.

We need to verify UDP integration for these critical services regularly, before deploying to a target environment.
While a UDP stub server is not a substitute for testing integration with a production UDP server, it can 
provide fast feedback of network UDP communication issues.  It can also be used to drive event-based-system tests,
by having a test listen to specific logging events, and drive test execution asynchronously by those events. 
(other article)

If the SUT log a lot of data, limited by UDP message size before a custom protocol to handle message ordering
on reading back the buffer.  To mitigate this and to support a simple TCP based server to handle interacting
with the test data
To verify integration the stub server could log requests in a buffer, and expose command messages to Read them back:

- UML
- start server - port, message read bytes
- Start TCP test server interface
- Commands
	- CLEAR BUFFER
	- GET BUFFER
- Create buffer
- UDP bind
- RECEIVE loop
	<- message
	-> TCP test server
		<- TCP test server adds to buffer
- UML


This simple server should allow for network protocol based testing 
- UML
	-> start UDP test service
TEST
	-> TCP clear buffer
	-> excercise SUT
		-> UDP
		-> UDP
	-> TCP GET BUFFER
	<- BUFFER
	assert buffer
- UML

Using the TCP allows for an asynchronous event based approach to system tests.

UML

UML


