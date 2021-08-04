<h4>Testing for Privilege Escalation</h4>
<p><b>ID: WSTG-ATHZ-03</b></p>
<p>During this phase, the tester should
verify that it is not possible for a user to modify their privileges or roles inside the application in ways that could allow privilege escalation attacks. The degree of escalation depends on what privileges the attacker is authorized to possess, and what privileges can be obtained in a successful exploit. <br>Objectives:</p>
<ul>
	<li>Identify injection points related to privilege manipulation.</li>
	<li>Fuzz or otherwise attempt to bypass security measures.</li>
</ul>
<p>Test for file traversal, and if you can bypass security checks using it. Also look for weak session IDs, and uncommon headers.</p>

<h4>Testing for IDORs</h4>
<p><b>ID: WSTG-ATHZ-04</b></p>
<p>Insecure Direct Object References (IDOR) occur when an application provides direct access to objects based on user-supplied input. As a result of this vulnerability attackers can bypass authorization and access resources in the system directly, for example database records or files. <br>Objectives: </p>
<ul>
	<li>Identify points where object references may occur.</li>
	<li>Assess the access control measures and if they’re vulnerable to IDOR.</li>
</ul>
<p>To test for this vulnerability the tester first needs to map out all locations in the application where user input is used to reference objects directly. For example, locations where user input is used to access a database row, a file, application pages and more. Next he can see if manipulation of values leads to access of other account information.</p>

<h3>Session Management Testing</h3>
<h4>Testing for Session Management Schema</h4>
<p><b>ID: WSTG-SESS-01</b></p>
<p>To avoid continuous authentication for each page of a website or service, web applications implement various mechanisms to store and validate credentials for a pre-determined timespan. These mechanisms are known as Session Management.</p>
<p>he overall goal is to be able to forge a
cookie that will be considered valid by the application and that will provide some kind of unauthorized access (session hijacking, privilege escalation, etc.) <br>Usually the main steps of the attack pattern are the following: </p>
<ul>
	<li>Cookie Collection: Collection of a sufficient number of cookie samples</li>
	<li>Cookie Reverse Enginnering: Analysis of the cookie generation algorithm</li>
	<li>Cookie Manipulation: Forging of a valid cookie in order to perform the attack.</li>
</ul>

<h4>Testing for Cookie Attributes</h4>
<p><b>ID: WSTG-SESS-02</b></p>
<p>Cookies can be set by the server, by including a Set-Cookie header in the HTTP response or via js. <br>Objective: Ensure that the proper security configuration is set for cookies.</p>

<p><b>Secure Attribute: </b>The Secure attribute tells the browser to only send the cookie if the request is being sent over a secure channel such as HTTPS. This will help protect the cookie from being passed in unencrypted requests.</p>
<p><b>HttpOnly Attribute: </b>The HttpOnly attribute is used to help prevent attacks such as session leakage, since it does not allow the cookie to be accessed via a client-side script such as JavaScript.</p>
<p><b>Domain Attribute: </b>The Domain attribute is used to compare the cookie’s domain against the domain of the server for which the HTTP request is being made. If the domain matches or if it is a subdomain, then the path attribute will be checked next.If the domain attribute is not set, then the hostname of the
server that generated the cookie is used as the default value of the domain. Moreover the top level domain can't set the cookie(such as .gov and .com). This is because they can set cookies for owasp.org and even for root-me.org. This shouldn't occur. A cookie set by a sub-domain/domain can be used for used by its sub-domains but not by another sub-domain/domain. </p>
<p><b>Path Attribute: </b>In addition to the domain, the URL path for which the cookie is valid can be specified. If the domain and path match, then the cookie will be sent in the request. For example, if the path attribute was set to the web server root / , then the application cookies will be sent to every application within the same domai</p>
<p><b>Expires Attribute: </b>This is used to <b>Set persistent cookies</b>,<b>limit the lifespan of the cookies</b>, <b>remove a cookie's forcefully by setting it to a past date.</b></p>
<p><b>Same Site Attribute: </b>The SameSite attribute is used to assert that a cookie ought not to be sent along with cross-site requests. This feature allows the server to mitigate the risk of cross-orgin information leakage. In some cases, it is used too as a risk reduction (or defense in depth mechanism) strategy to prevent cross-site request forgery attacks.</p>
<p><b>Cookie Prefixes: </b>Host Prefix: <b>Set-Cookie: __Host-SID=12345; Secure; Path=/</b>. <br>Secure Prefix: <b>__Secure-</b></p>
<h4>Testing for Session Fixation</h4>
<p><b>ID: WSTG-SESS-03</b></p>
<p>Session fixation is enabled by the insecure practice of preserving the same value of the session cookies before and after authentication. </p>
<p>In the generic exploit of session fixation vulnerabilities, an attacker can obtain a set of session cookies from the target website without first authenticating. The attacker can then force these cookies into the victim’s browser using different techniques. If the victim later authenticates at the target website and the cookies are not refreshed upon login, the victim will be identified by the session cookies chosen by the attacker. </p>

<h4>Testing for Exposed Session Variables</h4>
<p><b>ID: WSTG-SESS-04</b></p>
<p>The information here relates to how transport security applies to the transfer of sensitive Session ID data rather than data in general, and may be stricter than the caching and transport policies applied to the data served by the site. </p>
<p>Using a personal proxy, it is possible to ascertain the following about each request and response:</p>
<ul>
	<li>Protocol Used (HTTP/HTTPS)</li>
	<li>HTTP Headers</li>
	<li>Message Body(POST or page content)</li>
</ul>
<p>Each time Session ID data is passed between the client and the server, the protocol, cache, and privacy directives and body should be examined. Transport security here refers to Session IDs passed in GET or POST requests, message bodies, or other means over valid HTTP requests. Objectives: </p>
<ul>
	<li>Ensure that proper encryption is implemented.</li>
	<li>Review the caching configuration.</li>
	<li>Assess the channel and methods’ security.</li>
</ul>

<p>Test for encryption and session reuse vulnerabilities. Try to force https:// to http://. See if the session IDs are being encrypted and SSL is being used. Every time a user logs in, a different session token must be generated and the token must be sent via encrypted channel every time an HTTP request is being made.</p>
