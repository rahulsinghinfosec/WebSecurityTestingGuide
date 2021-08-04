<h4>Enumerate Infrastructure and Application Admin Interfaces</h4>
<p><b>ID: WSTG-CONF-05</b></p>
<p>The objective here is to identify any hidden applicaiton or interface that can be accessed only by the admin.This can be accomplished using:</p>
<ul>
	<li>Brute forcing</li>
	<li>Comments and hidden links in the source page.</li>
	<li>Review Server and application documentation</li>
	<li>Publically available information: (Eg Wordpress)</li>
	<li>Alternate Server Port</li>
	<li>Parameter Tampering</li>
</ul>

<h4>Test HTTP Methods</h4>
<p><b>ID: WSTG-CONF-06</b></p>
<p>HTTP offers a number of methods that can be used to perform actions on the web server.While GET and POST are by far the most common methods that are used to access information provided by a web server, HTTP allows several other (and somewhat less known) methods. Some of these can be used for nefarious purposes if the web server is misconfigured.</p>
<p>The most common methods used are GET and POST. But there are many others besides these 2 methods. Since the other methods are so rarely used, many developers do not know, or fail to take into consideration, how the web server or application framework’s implementation of these methods impact the security features of the application.</p>
<p>Our objective here it to:</p>
<ul>
	<li>Enumerate supported HTTP methods.</li>
	<li>Test for access control bypass.</li>
	<li>Test XST vulnerabilities.</li>
	<li>Test HTTP method overriding techniques.</li>
</ul>
<p>Eg. Leveraging the PUT method an attacker may be able to place arbitrary and potentially malicious content, into the system which may lead to remote code execution, defacing the site or denial of service.</p>

<p>Testing for Access Control Bypass: Generally you'll be issued a 3XX status code,when you try to access a restricted page. You may want to change the method type (to HEAD, POST, PUT, BILBAO, FOOBAR, CATS, etc.). If the server responds with a 2XX, then you've successfully bypassed the login page.</p>

<p>Testing for Cross-site Tampering Potential: The TRACE method, intended for testing and debugging, instructs the web server to reflect the received message back to the client.This method, while apparently harmless, can be successfully leveraged in some scenarios to steal legitimate users’ credentials. This attack technique was discovered by Jeremiah Grossman in 2003, in an attempt to bypass the HttpOnly attribute that aims to protect cookies from being accessed by JavaScript. However, the TRACE method can be used to bypass this protection and access the cookie even when this attribute is set.</p>
<p>Example: <br>
$ ncat www.victim.com 80 <br>
TRACE / HTTP/1.1 <br>
Host: www.victim.com <br>
Random: Header <br><br>
HTTP/1.1 200 OK <br>
Random: Header<br>As you can see that, the <b>Random: Header</b> is returned back as a part of the response. An attacker can send an XSS payload in the Random header.</p>

<p>Testing for HTTP Method Overriding : Some web frameworks provide a way to override the actual HTTP method in the request by emulating the missing HTTP verbs passing some custom header in the requests. The main purpose of this is to circumvent some middleware (e.g. proxy, firewall) limitation where methods allowed usually do not encompass verbs such as PUT or DELETE . The following alternative headers could be used to do such verb tunneling: X-HTTP-Method, X-HTTP-Method-Override, X-Method-Override.</p>

<h4>Test HTTP Strict Transport Security</h4>
<p><b>ID: WSTG-CONF-07</b></p>
<p>The HTTP Strict Transport Security (HSTS) feature lets a web application inform the browser through the use of a special response header that it should never establish a connection to the specified domain servers using un-encrypted HTTP. Instead, it should automatically establish all connection requests to access the site through HTTPS.</p>
<p>The HTTP strict transport security header uses two directives:<br>
<b>max-age</b> : to indicate the number of seconds that the browser should automatically convert all HTTP requests to HTTPS.<br><b>includeSubDomains</b>: to indicate that all related sub-domains must use HTTPS.</p>
<p>The presence of the HSTS header can be confirmed by examining the server’s response through an intercepting proxy or by using curl as follows:<br><b>$ curl -s -D- https://owasp.org | grep -i strict</b> <br>
<b>Strict-Transport-Security: max-age=31536000</b></p>

<h4>Test RIA Cross Domain Policy</h4>
<p><b>ID: WSTG-CONF-08</b></p>
<p>Rich Internet Applications (RIA) have adopted Adobe’s crossdomain.xml policy files to allow for controlled cross domain access to data and service consumption using technologies such as Oracle Java, Silverlight, and Adobe Flash(depreciated). Therefore, a domain can grant remote access to its services from a different domain. However, often the policy files that describe the access restrictions are poorly configured. Poor configuration of the policy files enables Cross-site Request Forgery attacks, and may allow third parties to access sensitive data meant for the user.</p>
<p><b>A cross-domain policy</b> file specifies the permissions that a web client such as Java, Adobe Flash, Adobe Reader, etc. use to access data across different domains.</p>
<p>Whenever a web client detects that a resource has to be requested from other domain, it will first look for a policy file in the target domain to determine if performing cross-domain requests, including headers, and socket-based connections are allowed.</p>
<p>How can cross domain policy files be abused?</p>
<ul>
	<li>Overly permissive cross-domain policies.</li>
	<li>Generating server responses that may be treated as cross-domain policy files.</li>
	<li>Using file upload functionality to upload files that may be treated as cross-domain policy files.</li>
</ul>
<p><b>crossdomain.xml</b> file is present at the root of the webpage. </p>
<h4>Test Files Permission</h4>
<p><b>ID: WSTG-CONF-09</b></p>
<p>When a resource is given a permissions setting that provides access to a wider range of actors than required, it could lead to the exposure of sensitive information, or the modification of that resource by unintended parties. This is especially dangerous when the resource is related to program configuration, execution, or sensitive user data.</p>
<p>How to test: In linux <b>ls and namei</b> can help you list all the file permissions.</p>

<h4>Test for Sub Domain Takeover</h4>
<p><b>ID: WSTG-CONF-10</b></p>
<p>A successful exploitation of this kind of vulnerability allows an adversary to claim and take control of the victim’s subdomain. This can occur if</p>
<ul>
	<li>The victim’s external DNS server subdomain record is configured to point to a non-existing or non-active resource/external service/endpoint</li>
	<li>The service provider hosting the resource/external service/endpoint does not handle subdomain ownership
verification properly.</li>
</ul>
<p>You can try various tools like: dnsrecon, dig CNAME, dig ns, sublist3r, recon-ng, OWASP Amass DNS Enueration,etc.</p>
