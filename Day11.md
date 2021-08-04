<h4>Testing for Format String Injection</h4>
<p><b>ID: WSTG-INPV-13</b></p>
<p>A format string is a null-terminated character sequence that also contains conversion specifiers interpreted or converted at runtime. If server-side code concatenates a user’s input with a format string, an attacker can append additional conversion specifiers to cause a runtime error, information disclosure, or buffer overflow. </p>
<p>The worst case for format strings vulnerabilities occur in languages that don’t check arguments and also include a %n specifier that writes to memory. These functions, if exploited by an attacker modifying a format string, could cause information disclosure and code execution:</p>
<ul>
	<li>C and C++ printf and similar methods fprintf, sprintf, snprintf</li>
	<li>Perl printf and sprintf</li>
</ul>
<p>These format string functions cannot write to memory, but attackers can still cause information disclosure by changing format strings to output values the developers did not intend to send:</p>
<ul>
	<li>Python 2.6 and 2.7 str.format and Python 3 unicode str.format can be modified by injecting strings that can point to other variables in memory. </li>
</ul>
<p>The following format string functions can cause runtime errors if the attacker adds conversion specifiers:</p>
<ul>
	<li>Java String.format and PrintStream.format</li>
	<li>PHP printf</li>
</ul>
<p>Static analysis tools like, <code>flawfinder in C/C++</code>,<code>Java: FindSecurityBugs rule FORMAT_STRING_MANIPULATION</code> and <code>PHP: String formatter Analyzer in phpsa</code>.</p>

<p>You can try to fuzz the input paramaters, to look for vulnerabilities. eg wfuzz</p>

<h4>Testing for Incubated Vulnerability</h4>
<p><b>ID: WSTG-INPV-14</b></p>
<p>Also often referred to as persistent attacks, incubated testing is a complex testing method that needs more than one data validation vulnerability to work. Incubated vulnerabilities are typically used to conduct “watering hole” attacks against users of legitimate web applications. They have the following characteristics: </p>
<ul>
	<li>The attack vector needs to be persisted in the first place, it needs to be stored in the persistence layer, and this would only occur if weak data validation was present or the data arrived into the system via another channel such as an admin console or directly via a backend batch process.</li>
	<li>Secondly, once the attack vector was “recalled” the vector would need to be executed successfully.</li>
</ul>
<p>For example: Stored XSS. A public forum allows an attacker to upload XSS payload,and the second step is the attack was recalled by the victim's browser but it should have the capability to execute XSS. <br>Similarly, the SQL/XPath Injection which allows an attacker to upload malicious file/script, which was later recalled by the server when fetching the contents to the users.</p>

<h4>Test for HTTP Splitting Smuggling</h4>
<p><b>ID: WSTG-INPV-15</b></p>
<p>HTTP Splitting exploits a lack of input sanitization which allows an intruder to insert CR and LF characters into the headers of the application response and to ‘split’ that answer into two different HTTP messages. The goal of the attack can vary from a cache poisoning to cross site scripting.</p>
<p>In HTTP Smuggling,the attacker exploits the fact that some specially crafted HTTP messages can be parsed and
interpreted in different ways depending on the agent that receives them. HTTP smuggling requires some level of
knowledge about the different agents that are handling the HTTP messages (web server, proxy, firewall) and therefore will be included only in the gray-box testing section. </p>

<h4>Testing for HTTP Incoming Requests</h4>
<p><b>ID: WSTG-INPV-16</b></p>
<p>This section describes how to monitor all incoming/outgoing HTTP requests on both client-side or server-side. The purpose of this testing is to verify if there is unnecessary or suspicious HTTP request sending in the background. </p>
<p>Test Objectives: Monitor all incoming and outgoing HTTP requests to the Web Server to inspect any suspicious requests. <br>Monitor HTTP traffic without changes of end user Browser proxy or client-side application.</p>
<p>How to test? You can use Reverse Proxy, Port Forwarding, TCP-level Network Capture. Fiddler or Charles are recommended since these tools can capture HTTP traffic and also easily edit/reply the modified HTTP requests</p>

<h4>Testing for Host Header Injection</h4>
<p><b>ID: WSTG-INPV-17</b></p>
<p>A web server commonly hosts several web applications on the same IP address, referring to each application via the virtual host. In an incoming HTTP request, web servers often dispatch the request to the target virtual host based on the value supplied in the Host header. Without proper validation of the header value, the attacker can supply invalid input to cause the web server to:</p>
<ul>
	<li>dispatch requests to the first virtual host on the list</li>
	<li>cause a redirect to an attacker-controlled domain</li>
	<li>perform web cache poisoning</li>
	<li>manipulate password reset functionality</li>
</ul>
<p>Test Objectives: Assess if the Host header is being parsed dynamically in the application and Bypass security controls that rely on the header.</p>
<p>Initial testing is as simple as supplying another domain (i.e. attacker.com ) into the Host header field. It is how the web server processes the header value that dictates the impact. The attack is valid when the web server processes the input to send the request to an attacker-controlled host that resides at the supplied domain, and not to an internal virtual host that resides on the web server. </p>
<p><b>X-Forwarded Host Header Bypass: </b>In the event that Host header injection is mitigated by checking for invalid input injected via the Host header, you can supply the value to the X-Forwarded-Host header. </p>

<h4>Testing for Server Side Template Injection</h4>
<p><b>ID: WSTG-INPV-18</b></p>
<p>Web applications commonly use server-side templating technologies (Jinja2, Twig, FreeMaker, etc.) to generate dynamic HTML responses.Server-side Template Injection vulnerabilities (SSTI) occur when user input is embedded in a template in an unsafe manner and results in remote code execution on the server. </p>

<h4>Testinf for Server Side Request Forgery</h4>
<p><b>ID: WSTG-INPV-19</b></p>
<p>Web applications often interact with internal or external resources. While you may expect that only the intended resource will be handling the data you send, improperly handled data may create a situation where injection attacks are possible. One type of injection attack is called Server-side Request Forgery (SSRF). A successful SSRF attack can grant the attacker access to restricted actions, internal services, or internal files within the application or the organization. In some cases, it can even lead to Remote Code Execution (RCE).</p>
<p>Example: <code>GET https://example.com/page?page=http://127.0.0.1/admin</code><br><code>GET https://example.com/page?page=file:///etc/passwd</code>. </p>
<h5>PDF Generators</h5>
<p>In some cases, a server may convert uploaded files to PDF format. Try injecting &lt;iframe&gt; , &lt;img&gt; , &lt;base&gt; , or &lt;script&gt; elements, or CSS url() functions pointing to internal services.</p>

<h3>Testing for Error Handling</h3>
<h4>Testing for Improper Error Handling</h4>
<p><b>ID: WSTG-ERRH-01</b></p>
<p>All types of applications (web apps, web servers, databases, etc.) will generate errors for various reasons. Developers often ignore handling these errors, or push away the idea that a user will ever try to trigger an error purposefully (e.g. sending a string where an integer is expected). When the developer only consider the happy path, they forget all other possible user-input the code can receive but can’t handle.</p>

<h4>Testing for Stack Traces</h4>
<p><b>ID: WSTG-ERRH-02</b></p>
<p>Similar to Testing for Improper Error Handling</p>

<h3>Testing for Weak Cryptography</h3>
<h4>Testing for Weak Transport Layer Security</h4>
<p><b>ID: WSTG-CRYP-01</b></p>
<p>When information is sent between the client and the server, it must be encrypted and protected in order to prevent an attacker from being able to read or modify it. This is most commonly done using HTTPS, which uses the Transport Layer Security (TLS) protocol. TLS also provides a way for the server to demonstrate to the client that they have connected to the correct server, by presenting a trusted digital certificate.</p>
<p>Test Objectives: Validate the service configuration, Review the digital certificate’s cryptographic strength and validit, Ensure that the TLS security is not bypassable and is properly implemented across the application.</p>
<p>Transport layer security related issues can be broadly split into the following areas:</p>
<p><b>Server Configuration</b></p>
<p>There are a large number of protocol versions, ciphers, and extensions supported by TLS. Many of these are
considered to be legacy, and have cryptographic weaknesses, such as those listed below</p>
<ul>
	<li>SSLv2</li>
	<li>SSLv3</li>
	<li>TLSv1.0</li>
	<li>EXPORT ciphers suite</li>
	<li>NULL ciphers</li>
	<li>Anonymous Ciphers</li>
	<li>RC4 ciphers</li>
	<li>CBC mode ciphers</li>
	<li>TLS Compression</li>
	<li>Weak DHE keys</li>
</ul>

<p><b>Digital Certificates</b></p>
<ul>
	<li>The key strength should be at least 2048 bits.</li>
	<li>The signature algorithm should be at least SHA-256. Legacy Algorithms like MD5 and SHA-1 should not be used.</li>
	<li>Be within the defined validity period.</li>
	<li>Be signed by a trusted certificate authority. (CA)</li>
	<li>Have a Subject Alternate Name (SAN) that matches the hostname of the system.</li>
</ul>
<p>Certificates can also leak information about the internal systems or domain names in the Issuer or SAN fields.</p>

<p><b>Application Vulnerabilities</b></p>
<p>Mixed Active Content: Mixed active content is when active resources (such as scripts to CSS) are loaded over unencrypted HTTP and included into a secure (HTTPS) page. This is dangerous because it would allow an attacker to modify these files (as they are sent unencrypted), which could allow them to execute arbitrary code (JavaScript or CSS) in the page. <small>Note: modern browsers will block active content being loaded from insecure sources into secure pages.</small></p>

<p><b>Automated Scanning</b></p>
<p>There are a large number of tools that can be used to identify weaknesses in the SSL/TLS configuration of a service.</p>
<ul>
	<li>Nmap</li>
	<li>sslscan</li>
	<li>OWASP O-Saft</li>
	<li>SSLLabs, sslyze, testssl.sh</li>
</ul>

<p><b>Manual Testing</b></p>
<p>It is also possible to carry out most checks manually, using command-line looks such as openssl s_client or
gnutls-cli to connect with specific protocols, ciphers or options.</p>
