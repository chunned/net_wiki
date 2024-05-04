[Source](https://www.netacad.com/courses/infrastructure-automation/devnet-associate)
## APIs
- Application Programming Interface
	- allows apps to talk to each other
- Synchronous API
	- respond to request directly, provide data immediately
	- used when data is readily available, i.e. stored in database/memory - server can fetch data instantly
- Asynchronous API
	- Provide response to let user know request has been received, but response doesn't contain data - server processes request (may take a while) and sends notif (or triggers callback) when data is ready
	- Used when request is an action that takes time for server to process or if data not readily available
## Common Architectural Styles
- Remote Procedure Call (RPC)
	- Request/response model
	- Lets app (client) make procedure call to another app (server)
	- Client typically unaware that the procedure request is being executed remotely; request made to a layer that hides those details
	- ![[Pasted image 20240112113419.png]]
	- Commonly, client makes synchronous req to the server and is blocked while server processes request; when server is done, sends response back which unblocks the process
	- Example implementations
		- XML-RPC, JSON-RPC, NFS, SOAP
- Simple Object Access Protocol (SOAP)
	- messaging protocol for communicating between apps that might be on different platforms/built with different langs
	- XML-based (considered an application of XML), developed by Microsoft
	- Commonly used with HTTP but can be applied to other protocols - SMTP, TCP, UDP, JMS
	- Messages contain four elements
		- Envelope, Header, Body, Fault ![[Pasted image 20240112120037.png]]
		- Envelope: root element, tells you the XML doc is a SOAP message
		- Header: optional; if present, must be first child of Envelope. Contains app-specific info like authorization, attributes
		- Body: contains data to be sent to server; must be XML and in its own namespace
		- Fault: optional, must be child of Body if present. Provides error/status info. Can only be one fault element in a SOAP message
- Representational State Transfer (REST)
	- Architectural design; can be applied to any protocol
	- Six constraints
		- **Client-server**: should be independent of each other
		- **Stateless**: requests from client must contain all info server needs to make the request, server can't maintain session states
		- **Cache**: responses from server must indicate whether response is cacheable - if it is, client can use the data for later requests
		- **Uniform interface**: must adhere to these 4 principles
			- Identification of resources - resource must be identified in the request as the object the server will access and manipulate
			- Manipulation of resources through representations - client receives representation from the server, which must contain enough data/metadata for client to be able to manipulate the resource
			- Self-descriptive messages - each message must contain all info for recipient to process the message
			- Hypermedia as the engine of application state - data sent by server must include additional actions/resources available for the client to access supplemental info about the resource
		- **Layered system**: hierarchical layers, each layer provides service only to the layer above it
		- **Code-on-demand**: optional; info returned by a REST service can include executable code
- URI/URL
	- `scheme:[//authority][/path][?query]`
	- ![[Pasted image 20240112130621.png]]
- Headers
	- Request headers - include additional info not related to content of the message, like Authorization
	- Entity headers - additional info that describe the content of the body of the message, i.e. Content-Type
	- Response headers - contain additional info not related to content of message, e.g. Set-Cookie, Cache-Control

## Sequence Diagrams
- aka Event Diagrams
- Interactions with REST APIs are typically a sequence of requests, not a single one
- Unified Modeling Language (UML)
- Y-axis is time, X-axis is "lifelines" - exchanges/messages, any element that can interact by receiving/sending a message
![[Pasted image 20240112131909.png]]

## Authentication
### Mechanisms
- Basic Auth
	- User/pass transmitted as header: `Authorization: Basic <user>:<pass>`
- Bearer Auth/Token Auth
	- `Authorization: Bearer <token>`
	- More secure; used with OAuth, SSO
- API key/token
	- `Authorization: <api key>` 
	- `Authorization: APIkey <api key>`
	- `Cookie: API_KEY=<api key>`
	- `Content-Type: application/json` (token transmitted in body)

## Authorization
- OAuth combines authentication + authorization
- Recommended form of authen/author for REST APIs
- Modern version is OAuth 2.0, not backwards compatible
- Lets pre-registered apps get authorization to perform REST API requests on user's behalf, without user needing to share credentials with the app itself
- Lets user provide creds directly to the authorization server (typically an IdP or IdS) to obtain access token that is shared with application
- Process of obtaining the token is called a *flow*; app then uses this token in the REST API as Bearer Auth

## Rate Limiting Algorithms
- No one standard way, but some common algorithms
- **Leaky bucket**: incoming reqs go into a queue, can come in at any rate but server processes at a fixed rate. If queue is full, request is rejected
- **Token bucket**: get x tokens per y time, accumulative. When req is made, server checks the bucket to make sure you have at least one token (and rejects if there are no tokens)
- **Fixed window counter**: Similar to token bucket, but uses a counter instead of tokens and is not accumulative. The time window is strict, i.e. starts based on clock, not when you make a request 
- **Sliding window counter**: Similar to fixed window, but the time window begins when you make a request, not based on the clock

## Webhooks
- Webhook = HTTP callback (POST to a specific URL that notifies an application of an event occurrence on some monitored resource)
- aka reverse APIs - applications subscribe to a webhook server by registering with the provider