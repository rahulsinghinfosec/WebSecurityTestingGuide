<h4>Test for CSS Injection</h4>
<p><b> ID: WSTG-CLNT-05 </b></p>
<p>A CSS Injection vulnerability involves the ability to inject arbitrary CSS code in the context of a trusted web site which is rendered inside a victim’s browser. The impact of this type of vulnerability varies based on the supplied CSS payload. It may lead to cross site scripting or data exfiltration. </p>
<p>This vulnerability occurs when the application allows user-supplied CSS to interfere with the application’s legitimate style sheets. Injecting code in the CSS context may provide an attacker with the ability to execute JavaScript in certain conditions, or to extract sensitive values using CSS selectors and functions able to generate HTTP requests. Generally, allowing users the ability to customize pages by supplying custom CSS files is a considerable risk.</p>

<p>Objectives: Identify CSS injection points and ssess the impact of the injection.</p>

<h4>Testing for Client Side Resource Manipulation</h4>
<p><b>ID: WSTG-CLNT-06</b></p>
<p>A client-side resource manipulation vulnerability is an input validation flaw. It occurs when an application accepts user-controlled input that specifies the path of a resource such as the source of an iframe, JavaScript, applet, or the handler of an XMLHttpRequest. This vulnerability consists of the ability to control the URLs that link to some resources present in a web page. The impact of this vulnerability varies, and it is usually adopted to conduct XSS attacks. This vulnerability makes it is possible to interfere with the expected application’s behavior by causing it to load and render malicious objects.</p>

<h4>Testing Cross Origin Resource Sharing</h4>
<p><b>ID: WSTG-CLNT-07</b></p>
<p>Cross origin resource sharing (CORS) is a mechanism that enables a web browser to perform cross-domain requests using the XMLHttpRequest L2 API in a controlled manner. In the past, the XMLHttpRequest L1 API only allowed requests to be sent within the same origin as it was restricted by the same origin policy.</p>
<p>Cross-origin requests have an origin header that identifies the domain initiating the request and is always sent to the server. CORS defines the protocol to use between a web browser and a server to determine whether a cross-origin request is allowed. HTTP headers are used to accomplish this.</p>
<p>The W3C CORS specification mandates that for non simple requests, such as requests other than GET or POST or
requests that uses credentials, a pre-flight OPTIONS request must be sent in advance to check if the type of request will have a bad impact on the data.</p>
<p>The origin header is always sent by the browser in a CORS request and indicates the origin of the request. The origin header can not be changed from JavaScript however relying on this header for Access Control checks is not a good idea as it may be spoofed outside the browser, so you still need to check that application-level protocols are used to protect sensitive data.</p>
<p>Access-Control-Allow-Origin is a response header used by a server to indicate which domains are allowed to read the response. Based on the CORS W3 Specification it is up to the client to determine and enforce the restriction of whether the client has access to the response data based on this header.</p>
<p>From a penetration testing perspective you should look for insecure configurations as for example using a * wildcard as value of the Access-Control-Allow-Origin header that means all domains are allowed.</p>

<h4>Testing for Cross Site Flashing</h4>
<p><b>ID: WSTG-CLNT-08</b></p>
<p>Flash are outdated and not being used anymore.</p>

<h4>Testing for Clickjacking</h4>
<p><b>ID: WSTG-CLNT-09</b></p>
<p>Clickjacking, a subset of UI redressing, is a malicious technique whereby a web user is deceived into interacting (in most cases by clicking) with something other than what the user believes they are interacting with. This type of attack, either alone or in conjunction with other attacks, could potentially send unauthorized commands or reveal confidential information while the victim is interacting with seemingly-harmless web pages.</p>
<p>A clickjacking attack uses seemingly-harmless features of HTML and JavaScript to force the victim to perform undesired actions, such as clicking an invisible button that performs an unintended operation. This is a client-side security issue that affects a variety of browsers and platforms. </p>

<h4>Testing WebSockets</h4>
<p><b>ID: WSTG-CLNT-10</b></p>
<p>Traditionally, the HTTP protocol only allows one request/response per TCP connection. Asynchronous JavaScript and XML (AJAX) allows clients to send and receive data asynchronously (in the background without a page refresh) to the server, however, AJAX requires the client to initiate the requests and wait for the server responses (half-duplex). </p>
<p>WebSockets allow the client or server to create a ‘full-duplex’ (two-way) communication channel, allowing the client and server to truly communicate asynchronously. WebSockets conduct their initial upgrade handshake over HTTP and from then on all communication is carried out over TCP channels by use of frames.</p>
<h5>Origin</h5>
<p>It is the server’s responsibility to verify the Origin header in the initial HTTP WebSocket handshake. If the server does not validate the origin header in the initial WebSocket handshake, the WebSocket server may accept connections from any origin. This could allow attackers to communicate with the WebSocket server cross-domain allowing for CSRF-like issues. </p>
<h5>Confidentiality & Integrity</h5>
<p>WebSockets can be used over unencrypted TCP or over encrypted TLS. To use unencrypted WebSockets the ws://
URI scheme is used (default port 80), to use encrypted (TLS) WebSockets the wss:// URI scheme is used (default
port 443).</p>
<p>Objectives: Identify the usage of WebSockets and assess its implementation by using the same tests on normal HTTP channels.</p>
<h5>How to test</h5>
<p>Inspect the client-side source code for the ws:// or wss:// URI scheme. Try using a proxy or the developer options tab. </p>
<p>Using a WebSocket client (one can be found in the Tools section below) attempt to connect to the remote
WebSocket server. If a connection is established the server may not be checking the origin header of the
WebSocket handshake.</p>
<p>Confidentiality & Integrity: Check that the WebSocket connection is using SSL to transport sensitive information wss:// . Check the SSL Implementation for security issues (Valid Certificate, BEAST, CRIME, RC4, etc).</p>
<p>Authentication: WebSockets do not handle authentication, normal black-box authentication tests should be carried out.</p>
<p>Authorization: WebSockets do not handle authorization, normal black-box authorization tests should be carried out.</p>
<p>Input Sanitization: Use ZAP’s WebSocket tab to replay and fuzz WebSocket request and responses</p>

<h4>Testing Web Messaging</h4>
<p><b>ID: WSTG-CLNT-11</b></p>
<p>Web Messaging (also known as Cross Document Messaging) allows applications running on different domains to
communicate in a secure manner. Due to the same origin policy, applications running on different domains could not communicate with each other. This restriction within the browser is in place to prevent a malicious website from reading confidential data from other iframes, tabs, etc; however, there are some legitimate cases where two trusted websites need to exchange data with each other. To meet this need, Cross Document Messaging was introduced in the WHATWG HTML5 draft specification and was implemented in all major browsers. It enables secure communications between multiple origins across iframes, tabs and windows. </p>

<h4>Testing Browser Storage</h4>
<p><b>ID: WSTG-CLNT-12</b></p>
<p>Browsers provide the following client-side storage mechanisms for developers to store and retrieve data:</p>
<ul>
	<li>Local Storage</li>
	<li>Session Storage</li>
	<li>IndexedDB</li>
	<li>Cookies</li>
</ul>
<p>Objectives: Determine whether the website is storing sensitive data in client-side storage and the code handling of the storage objects should be examined for possibilities of injection attacks, such as utilizing
unvalidated input or vulnerable libraries.</p>

<h5>How to test?</h5>
<p>Local Storage: window.localStorage is a global property that implements the Web Storage API and provides persistent key-value storage in the browser. Both the keys and values can only be strings, so any non-string values must be converted to strings first before storing them, usually done via JSON.stringify.</p>
<p>Session Storage: window.sessionStorage is a global property that implements the Web Storage API and provides ephemeral key-value storage in the browser.</p>
<p>IndexedDB: IndexedDB is a transactional, object-oriented database intended for structured data. An IndexedDB database can have multiple object stores and each object store can have multiple objects.
In contrast to Local Storage and Session Storage, IndexedDB can store more than just strings. Any objects supported by the structured clone algorithm can be stored in IndexedDB.</p>

<h4>Testing for Cross Site Script Inclusion</h4>
<p><b>ID: WSTG-CLNT-13</b></p>
<p>Cross Site Script Inclusion (XSSI) vulnerability allows sensitive data leakage across-origin or cross-domain
boundaries. Sensitive data could include authentication-related data (login states, cookies, auth tokens, session IDs,etc.) or user’s personal or sensitive personal data (email addresses, phone numbers, credit card details, social security numbers, etc.). XSSI is a client-side attack similar to Cross Site Request Forgery (CSRF) but has a different purpose. Where CSRF uses the authenticated user context to execute certain state-changing actions inside a victim’s page.Where CSRF uses the authenticated user context to execute certain state-changing actions inside a victim’s page, XSSI instead uses JavaScript on the
client-side to leak sensitive data from authenticated sessions. </p>


<h3>API Testing</h3>
<h4>Testing GraphQL</h4>
<p><b>ID: WSTG-APIT-01</b></p>
<p>GraphQL has become very popular in modern APIs. It provides simplicity and nested objects, which facilitate faster development. While every technology has advantages, it can also expose the application to new attack surfaces. The purpose of this scenario is to provide some common misconfigurations and attack vectors on applications that utilize GraphQL.</p>
<p>Objectives: Assess that a secure and production-ready configuration is deployed. Validate all input fields against generic attacks. Ensure that proper access controls are applied.</p>
<p>There are a lot more resources available on pen testing GraphQL. Refer those.</p>
