# Event Based System Testing

(Who is target audience)?

Higher level tests such as ones excersing a systems public interface, the same one which external users of the product 
will be exercising, are notirous for being slow (time to execute), flaky (false failures, inconsistant failures) and 
often difficult to maintain (tests data sets, long feedback loops)  Because of the difficulty in creating and maintaining 
reliable higher level tests, system testing is often performed by developers as part of development or by a QA department
before a release is allowed. While developer testing is implicitly required with creating any sort of software, with enough
investment and the application of maintainable techniques, explicit QA based software release gating can be removed 
from the software development lifecycle.

Focus on system tests involving asynchronous systems.  An asynchronous system is one which performs work outside of 
the context of a request:

**Diagram Synchronous**

Client -> System
Client <- System


**Diagram Asyncrhronous**


## problem

Test which exercise asynchronous systems need a mechanism for qualifying when it's time to make an assertion.

Test essentially performs an action on a system, and verifies a certain state.  With asynchronous systems, when should
the state verification be performed?

Don't want to put test specific logic in code.  If it is an explicit logical branch it can significantly increase the
amount of 

Maximize system for testability while minimizing any test specific logic because of the maintanence cost incurred.


## Solutions

### Timeouts

### Polling

###

