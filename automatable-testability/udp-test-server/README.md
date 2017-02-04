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
with the test data.

### UDP stub server components

![UDP Integration Service Components](stub-servers.png)

The UDP stub server read loop:

  - <- Receives message 
  - -> Sends message to TCP test server


### Test flow using UDP stub server

This simple server should allow for network protocol based testing.  The chart below 
illustrates a common test flow that allows assertions based on messages emitted by the
SUT.

![UDP Integration Test Workflow](integration-server-testing.png)


### Overriding UDP logging as asynchronous test driver

Since logging usually contains important program state information, it can be used to
asynchronously drive test, if the server exposes a way to notify a client of events
it receives.  Using an asynchronous event based approach to drive service tests helps
to minimize timing based flakiness, as the tests needs to apply inputs and make assertions
based on states of the SUT.

Using the UDP service to listen to event logs and exposing a persistent connection for the
TCP status server to push UDP message receives to a client, is a way to achieve this
without modifying the SUT to directly support.

- client supports syslog handler
- state change level is logged at syslog handler
- test opens a persistent connection to TCP status server
- when TCP status server receives updates it pushes those to the test client
- test client performs testing steps or assertions based on messages received

This process can be illustrated in the following diagram:

![Async UDP test driver](udp-async-test-driver.png)

With the persistent connection, the test now has real time, instantaneous insight
into what the SUT is doing.
