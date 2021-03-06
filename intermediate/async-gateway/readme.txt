Gateway provides a convenient way to expose a Proxy over a service-interface thus giving you a POJO-based access 
to a messaging system (based on objects in your own domain, or primitives/Strings, etc).
However when you invoke a method you expect the method to return. And since gateway's method call represents a 
contract with the messaging system which states that for each request there will always be a reply you must always 
guarantee that your message flow is in compliance with such contract. And in a lot of cases you can based on how your 
flow is structured. But what about the cases where you can't (e.g, message was filtered out and discarded or routed into 
a unidirectional sub-flow)?
With Spring Integration 2.0 we are introducing support for an Asynchronous Gateway which is
a convenient way to initiate flows where you may not know if a reply is expected or how long will it take for it
to arrive.
A natural way to handle these types of scenarios in Java would be relying upon java.util.concurrent.Future
instances, and that is exactly what Spring Integration uses to support an Asynchronous Gateway.

This example demonstrates how you can apply Asynchronous Gateway based on the simple use case:

We are sending request to a MathService to multiply random numbers by 2. As you can see from the configuration there is a filter that 
discards any request for the number that is less then a 100. This means that there will be no replies coming for the requests with 
numbers less then 100.
Typically when using the regular Gateway the gateway method would lock until a timeout where here responses are coming back right away as Java Futures
which we evaluate.

To run this sample simply execute To run this sample simply execute org.springframework.integration.samples.async.gateway.AsyncGatewayTest

You should see the following output:

INFO : org.springframework.integration.samples.async.gateway.AsyncGatewayTest - Result of multiplication of 107 by 2 is 214
INFO : org.springframework.integration.samples.async.gateway.AsyncGatewayTest - Result of multiplication of 146 by 2 is 292
INFO : org.springframework.integration.samples.async.gateway.AsyncGatewayTest - Result of multiplication of 189 by 2 is 378
INFO : org.springframework.integration.samples.async.gateway.AsyncGatewayTest - Result of multiplication of 130 by 2 is 260
. . . . .
INFO : org.springframework.integration.samples.async.gateway.AsyncGatewayTest - Multiplication of 38 by 2 is can not be accomplished in 20 seconds
INFO : org.springframework.integration.samples.async.gateway.AsyncGatewayTest - Multiplication of 39 by 2 is can not be accomplished in 20 seconds
INFO : org.springframework.integration.samples.async.gateway.AsyncGatewayTest - Multiplication of 36 by 2 is can not be accomplished in 20 seconds
INFO : org.springframework.integration.samples.async.gateway.AsyncGatewayTest - Multiplication of 37 by 2 is can not be accomplished in 20 seconds
