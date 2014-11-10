---
layout: post
title:  "Intro Web Architecture"
date:   2014-06-01 12:00:00
categories: jekyll update
img: "../img/web.png"
---
##The Internet
The Internet is a series of routers and wires that transmits information according to a set of rules known as the Internet Protocol Suite (commonly known as TCP/IP, named for the ‘Transmission Control Protocol” and “Internet Protocol”).

The physical infrastructure is provided by a number of institutions known as Internet Service Providers (Verizon, AT&T, IBM, etc.). Any device connected to the internet ultimately goes through an ISP.

Every machine that is connected to the Internet has a unique Internet Protocol (IP) address. When information is transferred via the Internet, the senders and recipients are identified using their IP addresses.

Note that the Internet is not the same as the web. The web is a network of linked webpages which are accessed via the Internet. In this sense, the web is an application which makes use of the Internet.

##Client-Server Interaction
Clients and servers are both computers, with unique IP addresses, which are connected to the Internet. The client is the end-user which makes requests of the server to share its content or service function. The purpose of the server is to host content to be accessed by the client; the server shares information, the client does not.

When a person accesses a website, their computer is the client. The machine on which the website is hosted is the server.

##Web App Structure
A web application is software which performs some task for the user and is accessible through the Internet. Web applications are frequently described as having two basic components, the back end and front end.

The back end is a reference to the server related elements of the application. As client requests are made, the backend determines what information should be transmitted the client.

The front end refers to the client-facing elements of the application. It is what the user of the application sees and interacts with. It renders information supplied by the back end of the application and transmits information, which is given by user interaction with the User Interface (UI), to the back end.

In short, the front end is manipulated by the user while the back end resides on the server.

##Web App Interaction
Users get content from the server using a web browser. The browser is a software application which interprets a variety of content types (webpages, videos, pictures, etc). The user identifies where to look for the content they want by the URL (Uniform Resource Locator).

In general, the URL is formatted as (protocol)://(host):(port)/(resource path)?(query)

##The DNS
We said earlier that the servers where information is pulled from are identified by their unique IP address. But where in the URL do we identify the IP address of the machine from which we want to get information? Each domain name (the host piece of the URL) is connected to a server (or collection of servers) that has an IP address associated with it.

The Domain Name Service (DNS for short) is a directory which maps the more easily remembered domain names that we type into the browser (www.nytimes.com for example), to the less easily remembered IP addresses of the servers which host the desired content (170.149.168.130 for the New York Times website).

##Hypertext Transfer Protocol
As previously stated, HTTP is a set of rules for requesting and receiving web content. HTTP is said to be stateless because it treats each information request as independent of all previous requests.

The URL identifies a host with which to communicate. The specific action to be taken is specified through HTTP verbs. These standard request verbs are GET (fetch an existing resource), POST (create a new resource), PUT (update an existing resource), and DELETE (remove an existing resource).

The response from the server will be the message payload(ideally the user requested content) along with a status code to inform the client of the status of their request (successful, redirecting, error, etc).

Every client server interaction occurs according to these request/ response pairs. The URL + HTTP verb makes the request and the message payload + status code are the response.
