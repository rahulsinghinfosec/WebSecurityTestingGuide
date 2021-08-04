<h4>Testing for Session Hijacking</h4>
<p><b>ID: WSTG-SESS-09</b></p>
<p>An attacker who gets access to user session cookies can impersonate them by presenting such cookies. This attack is known as session hijacking.  Cookie should be set with Secure Attribute.</p>
<p>Alternatively, session hijacking can be prevented by banning use of HTTP using HSTS.</p>

<h3>Input Validation Testing</h3>
<h4>Testing for reflected Cross Site Scripting</h4>
<p><b>ID: WSTG-INPV-01</b></p>
<p>Reflected Cross-site Scripting (XSS) occur when an attacker injects browser executable code. The injected attack is not stored within the application itself; it is non-persistent and only impacts users who
open a maliciously crafted link or third-party web page. Reflected XSS attacks are also known as
non-persistent XSS attacks and, since the attack payload is delivered and executed via a single request and response, they are also referred to as first-order or type 1 XSS.</p>
<p>Test Objectives: Identify variables that are reflected in responses.<br>Assess the input they accept and the encoding that gets applied on return (if any).</p>
<p>There can be blacklists filters applied. So, you can use encoding (instead of < or >) or use recursive queries (eg &lt;scr&lt;script&gt;ipt&gt;alert(document.cookie)&lt;/script&gt;</p>
<p>Leveraging HTTP Paramater Pollution: <br>Regular Attack-> http://example/page.php?param=&lt;script&gt;[...]&tl;/script&gt; <br> Using HPP -> http://example/page.php?param=&lt;script&param=&gt;[...]&lt;/&param=script&gt;</p>
<p>You can even try XSS Filter Evasion Cheat Sheet (by OWASP and others)</p>

<h4>Testing for Stored XSS</h4>
<p><b>ID: WSTG-INPV-02</b></p>
<p>Stored Cross-site Scripting (XSS) is the most dangerous type of Cross Site Scripting. Web applications that allow users to store data are potentially exposed to this type of attack. Stored XSS occurs when a web application gathers input from a user which might be malicious, and then stores that input in a data store for later use. The input that is stored is not correctly filtered. As a consequence, the malicious data
will appear to be part of the web site and run within the user’s browser under the privileges of the web application. Since this vulnerability typically involves at least two requests to the application, this may also called second-order XSS.</p>
<p>Stored XSS can be exploited by advanced JavaScript exploitation frameworks such as BeEF and XSS Proxy.</p>
<p>File Upload: If the web application allows file upload, it is important to check if it is possible to upload HTML content. For instance, if HTML or TXT files are allowed, XSS payload can be injected in the file uploaded.</p>
<p>The pen-tester should also verify if the file upload allows setting arbitrary MIME types. This design flaw can be exploited in browser MIME mishandling attacks. For instance, innocuous-looking files like JPG and GIF can contain an XSS payload that is executed when they are loaded by the browser. This is possible when the
MIME type for an image such as image/gif can instead be set to text/html . In this case the file will be treated by the client browser as HTML.</p>
<p>Example:
	<code>Content-Disposition: form-data; name="uploadfile1"; filename="C:\Documents and Settings\test\Desktop\test.gif"</code><br>
    <code>Content-Type: text/html</code><br>
    <code>&tl;script&gt;alert(document.cookie)&tl;/script&gt;</code> </p>
<h4>Testing for HTTP Verb Tampering</h4>
<p><b>ID: WSTG-INPV-03</b></p>
<p>This is merged into <b>Test HTTP Methods</b></p>

<h4>Testing for HTTP Parameter Pollution</h4>
<p><b>ID: WSTG-INPV-04</b></p>
<p>HTTP Parameter Pollution tests the applications response to receiving multiple HTTP parameters with the same name; for example, if the parameter <b>username</b> is included in the GET or POST parameters twice.</p>
<p>Supplying multiple HTTP parameters with the same name may cause an application to interpret values in unanticipated ways. By exploiting these effects, an attacker may be able to bypass input validation, trigger application errors or modify internal variables values. </p>
<p>By itself, this is not necessarily an indication of vulnerability. However, if the developer is not aware of the problem, the presence of duplicated parameters may produce an anomalous behavior in the application that can be potentially exploited by an attacker. <br>Test for Server Side HPP:</p>
<ol>
	<li>Submit the request: <b>page?par1=val1</b></li>
	<li>Submit another request, with a tampered value: <b>page?par1=HPP_TEST1</b></li>
	<li>Submit final request: <b>page?par1=HTTP_TEST1&par1=HTTP_TEST2</b></li>
</ol>
<p>Compare the responses obtained during all previous steps. If the response from (3) is different from (1) and the response from (3) is also different from (2), there is an impedance mismatch that may be eventually abused to trigger HPP vulnerabilities. <br>Test for Client Side HPP</p>

<p>To test for HPP client-side vulnerabilities, identify any form or action that allows user input and shows a result of that input back to the user. A search page is ideal, but a login box might not work (as it might not show an invalid username back to the user). </p>
<p>Similarly to server-side HPP, pollute each HTTP parameter with %26HPP_TEST and look for url-decoded occurrences of the user-supplied payload: eg &HPP_TEST, &amp ;HPP_TEST, etc.</p>

<h4>Testing for SQL injection</h4>
<p><b>ID: WSTG-INPV-05</b></p>
<p>SQL injection testing checks if it is possible to inject data into the application so that it executes a user-controlled SQL query in the database. Testers find a SQL injection vulnerability if the application uses user input to create SQL queries without proper input validation. A successful exploitation of this class of vulnerability allows an unauthorized user to access or manipulate data in the database.</p>
<p>SQL attacks can be divided into: </p>
<ul>
	<li>Inband</li>
	<li>Out-of-Band</li>
	<li>Inferential or Blind</li>
</ul>
<p>Techniques used to exploit SQL injection</p>
<ul>
	<li>Union Based</li>
	<li>Boolean Based</li>
	<li>Error Based</li>
	<li>Out-of-Band</li>
	<li>Time Delay</li>
</ul>
