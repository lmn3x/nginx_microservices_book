In microservice each app is a self contained app that speak with others with API

each has it's own data store.

it's easier to run them in multiple servers.

Monolithic apps problems:
- large code base make it hard to add new feauter in future.

- you stuck with framwork XYZ which you start with.

- long startup time!

- because startup time is long, its hard for CD(countinios dlevery)

- you stuck with needing too much hardware if some part of your app needs CPU and some other part needs lot's of memory.

- another problem is reliability. If a module face a bug, entire system went down.

- that's it :)

-----

each service (typically) has a set of distinc feauters of functionalities.

each microservice is a mini application.

seperate functional parts to services.



API Gateway:
- load balancing
- caching
- access control
- api metring
- monitoring


each service has its own db and can have its own database type.


Microservices Benefits:
- divide the big app to set of services 
- single (each) service is faste to develope, easier to understand and maintain.
- each service can have its own team for develope or whatever tool/language they ant
- each app can develope independently
- each app can scaled independetly.

microservices cons:
- too much services is not fine
- the fact that it is a distributed system
- partitioned databases
- complex testing(compare to monolith)
- the case of updating depandant services => if a->b->c then the update is this way `c->b->a`

- complex deployment 
    + to solve this use:
        - pass
        - k8s and docker


API Gateway
- ways to request services:
    - direct sending request
        - its too complex
        - its unefficent
        - some services may use other portocols
        - its get difficalt to refactore
    - API GateWay is a server as a single entry point for the system.
        - its similare to Facade in OOP
        - request routing 
        - composition
        - portocol translation
        - ApiGaeway recive a single request and send requests to services it needed.

pros of api gateway 
- it capsulate internal structure 

cons:
- its another part that need to develop,deploy and etc...

____

- for developing apigateway, need to use async none blocking I/O platforms like `nodejs`

- the api gateway need to perform independent requests concurently.
- its beter to develope it in reactive style.

- as its distrubuated it should use a inned-process cominucation mecanism.
    - async, message bassed
    - sync
    

- Service discovery
    - server side
    - client side

> handeling partiual faliures: when a service is down or slow, it should not effect other services

____
### Inner Process Comminucation

in microservices architecture, each service instance is typiclly a proccess
(in monolith, comminucations are language level methods or functions)

- IPC
    - one-to-one Interaction
        - request/response (might block while waiting)
        - notifications
        - request/async response (won't block while waiting)
    - one-to-many (async)
        - publish/subscribe (push a notif to zero or more)
        - publish/async response

# todo: check if it was before `I` page

[figure 3-2]

- Defining a service api:
    - one way is to use api first approach 
        - the nature of api depends on what IPC you use.
- Evolving API's
    - one way for handle updates (major updates) is to use apu versioning.
    - deploy on instances each handle pirticular version.
- handling partial failure:
    - network time outs -> always use time outs.
    - rate limite for out standing requests.
- circut breaker patterns:
    - track the number of successful and failed requests.
    - if error rate exceeds a configured threshhold 
    - so its a circuit breaker;-> further attemps should fail immediatly.
    - if too many request fail,sending new requests is pointless.

- provide fallbacks
    - have a fall back logic-> e.g: send cached data.

----
IPC technologies: 
- HTTP:   
    - REST or thrift
- async/message base
    - AMQP
    - STOMP

- async - message base:
    - clinet send a message (async) not waiting for response 
    - if there is a response, send that as a message to.

- Message 
    - header
    - body

- messages exchange over channels
- any number of produsers can send message.
- any number of consumers can recive message.

- channels:
    - point-to-point:
        - a p2p 
