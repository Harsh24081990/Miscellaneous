### API (Application Programming Interface)
- An API is a broad term that refers to any interface that allows two or more applications or systems to communicate with each other. It defines a set of rules and protocols that specify how different software components should interact.
-----------------------------------------------------------------------------------
### Types of APIs:
	• Web APIs: Allows applications to communicate over the web using HTTP/HTTPS protocols (e.g., REST, SOAP, GraphQL).
	• Library APIs: Provides functions and methods in a programming language that developers can use directly in their applications. (e.g. PySpark, Pandas etc.)
	• Operating System APIs: Interfaces to interact with the operating system (e.g., file system APIs, device APIs).
	• Hardware APIs: Enables communication with hardware devices.
------------------------------------------------------------------------------------------------
### REST API (Representational State Transfer API):
Definition: A REST API is a specific type of web API that follows the principles of REST architecture. REST APIs are designed for communication over the web using HTTP/HTTPS and rely on a stateless, client-server communication model.

REST APIs are widely used for building web services, enabling client applications to retrieve or modify resources from a server (such as data in a database) via standardized HTTP methods. REST APIs allow applications to access and manipulate resources (data) in a lightweight and scalable way, often using JSON as the data format.

- --> Resources (e.g., data objects, files) are represented with URIs (Uniform Resource Identifiers), and actions are performed using HTTP methods.
HTTP methods: REST APIs primarily use:<br>
**	• GET: Retrieve data.<br>
	• POST: Create data.<br>
	• PUT: Update data.<br>
	• DELETE: Remove data.<br>**
------------------------------------------------------------------------------------------------
- Example:
	A REST API for a weather service might allow you to retrieve current weather information by sending a GET request to https://api.weather.com/current?city=London

-----------------------------------------------------------------------------------
