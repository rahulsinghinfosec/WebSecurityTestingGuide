<h4>Test Number of Times a Function Can Be Used Limits</h4>
<p><b>ID: WSTG-BUSL-05</b></p>
<p>Many of the problems that applications are solving require limits to the number of times a function can be used or action can be executed. Applications must be “smart enough” to not allow the user to exceed their limit on the use of these functions since in many cases each time the function is used the user may gain some type of benefit that must be accounted for to properly compensate the owner. </p>
<p>Objectives: Identify functions that must set limits to the times they can be called,and assess if there is a logical limit set on the functions and if it is properly validated.</p>

<h4>Testing for Circumvention of Work Flows</h4>
<p><b>ID: WSTG-BUSL-06</b></p>
<p>Workflow vulnerabilities involve any type of vulnerability that allows the attacker to misuse an application/system in a way that will allow them to circumvent (not follow) the designed/intended workflow.</p>
<p>The application’s business logic must require that the user complete specific steps in the correct/specific order and if the workflow is terminated without correctly completing, all actions and spawned actions are “rolled back” or canceled. Vulnerabilities related to the circumvention of workflows or bypassing the correct business logic workflow are unique in that they are very application/system specific and careful manual misuse cases must be developed using requirements and use cases.</p>
<p>Example: Many of us receive so type of “club/loyalty points” for purchases from grocery stores and gas stations. Suppose a user was able to start a transaction linked to their account and then after points have been added to their club/loyalty account cancel out of the transaction or remove items from their “basket” and tender. In this case the system either should not apply points/credits to the account until it is tendered or points/credits should be “rolled back” if the point/credit increment does not match the final tender. With this in mind, an attacker may start transactions and cancel them to build their point levels without actually buying anything.</p>

<h4>Test Applications against Application Misuse</h4>
<p><b>ID: WSTG-BUSL-07</b></p>
<p>The misuse and invalid use of of valid functionality can identify attacks attempting to enumerate the web application, identify weaknesses, and exploit vulnerabilities. Tests should be undertaken to determine whether there are application-layer defensive mechanisms in place to protect the application.</p>
<p>The lack of active defenses allows an attacker to hunt for vulnerabilities without any recourse. The application’s owner will thus not know their application is under attack. <br>Objectives:</p>

<ul>
	<li>Generate notes from all tests conducted against the system.</li>
	<li>Review which tests had a different functionality based on aggressive input.</li>
	<li>Understand the defenses in place and verify if they are enough to protect the system against bypassing
techniques.</li>
</ul>

<h4>Test Upload of Unexpected File Types</h4>
<p><b>ID: WSTG-BUSL-08</b></p>
<p>Many applications’ business processes allow for the upload and manipulation of data that is submitted via files. But the business process must check the files and only allow certain “approved” file types. Deciding what files are “approved” is determined by the business logic and is application/system specific. The risk in that by allowing users to upload files, attackers may submit an unexpected file type that that could be executed and adversely impact the application or system through attacks that may deface the web site, perform remote commands, browse the system files, browse the local resources, attack other servers, or exploit the local vulnerabilities, just to name a few.</p>
<p>Suppose a picture sharing application allows users to upload a .gif or .jpg graphic file to the web site. What if an attacker is able to upload an HTML file with a &lt;script&gt; tag in it or PHP file? The system may move the file from a temporary location to the final location where the PHP code can now be executed against the application or system. <br>Objectives:</p>

<ul>
	<li>Review the project documentation for file types that are rejected by the system</li>
	<li>Verify that the unwelcomed file types are rejected and handled safely.</li>
	<li>Verify that file batch uploads are secure and do not allow any bypass against the set security measures.</li>
</ul>

<h4>Test Upload of Malicious Files</h4>
<p><b>ID: WSTG-BUSL-09</b></p>
<p>Many application’s business processes allow users to upload data to them. Although input validation is widely understood for text-based input fields, it is more complicated to implement when files are accepted. Although many sites implement simple restrictions based on a list of permitted (or blocked) extensions, this is not sufficient to prevent attackers from uploading legitimate file types that have malicious contents.</p>

<p>This is different from uploading unexpected files in that while the file type may be accepted the file may still be malicious to the system. </p>
<p>Example: A common example of this vulnerability is an application such as a blog or forum that allows users to upload images and other media files. While these are considered safe, if an attacker is able to upload executable code (such as a PHP script), this could allow them to execute operating system commands, read and modify information in the filesystem, access the back end database and fully compromise the server. <br>Objectives:</p>

<ul>
	<li>Identify the file upload functionality.</li>
	<li>Review the project documentation to identify what file types are considered acceptable, and what types would be considered dangerous or malicious.If documentation is not available then consider what would be appropriate based on the purpose of the application.</li>
	<li>Determine how the uploaded files are processed.</li>
	<li>Obtain or create a set of malicious files for testing.</li>
	<li>Try to upload the malicious files to the application and determine whether it is accepted and processed.</li>
</ul>

<h3>Client Side Testing</h3>
<h4>Testing for DOM-Based Cross Site Scripting</h4>
<p><b>ID: WSTG-CLNT-01</b></p>
<p>DOM-based cross-site scripting is the de-facto name for XSS bugs that are the result of active browser-side content on a page, typically JavaScript, obtaining user input through a source and using it in a sink, leading to the execution of injected code.</p>
<p>Due to their nature, DOM-based XSS vulnerabilities can be executed in many instances without the server being able to determine what is actually being executed. This may make many of the general XSS filtering and detection techniques impotent to such attacks.</p>
<p>This hypothetical example uses the following client-side code: <code>&lt;script&gt; document.write("Site is at: " + document.location.href + "."); &lt;script&gt;</code></p>
<p>An attacker may append #&lt;script&gt;alert('xss')&lt;/script&gt; <br>Objectives: Identify DOM Sinks, Build payloads that pertain to every sink type.</p>

<p>Often aautomated testing will not detect areas that may be susceptible to DOM-based XSS unless the testing
tool can perform additional analysis of the client-side code. They generally use payloads and wait for the server's response to refeclt their payload. This is not always the case with DOM based XSS, as many a times they are used in the client side.</p>

<h4>Testing for javaScript Exectution</h4>
<p><b>ID: WSTG-CLNT-02</b></p>
<p>A JavaScript injection vulnerability is a subtype of cross site scripting (XSS) that involves the ability to inject arbitrary JavaScript code that is executed by the application inside the victim’s browser. This vulnerability can have many consequences, like the disclosure of a user’s session cookies that could be used to impersonate the victim, or, more generally, it can allow the attacker to modify the page content seen by the victims or the application’s behavior.</p>

<p>Here is an example of a script that does not perform any validation of the variable rr . The variable contains user-supplied input via the query string, and additionally does not apply any form of encoding:</p>
<p><code>var rr = location.search.substring(1); if(rr) { window.location=decodeURIComponent(rr); }. </code>This implies that an attacker could inject JavaScript code simply by submitting the following query string:
www.victim.com/?javascript:alert(1) .</p>
<p>The test Objectives are: Identify sinks and possible JavaScript injection points.</p>

<h4>Test for HTML Injection</h4>
<p><b>ID: WSTG-CLNT-03</b></p>
<p>HTML injection is a type of injection vulnerability that occurs when a user is able to control an input point and is able to inject arbitrary HTML code into a vulnerable web page. This vulnerability can have many consequences, like disclosure of a user’s session cookies that could be used to impersonate the victim, or, more generally, it can allow the attacker to modify the page content seen by the victims.</p>
<p>This vulnerability occurs when user input is not correctly sanitized and the output is not encoded. An injection allows the attacker to send a malicious HTML page to a victim. The targeted browser will not be able to distinguish (trust) legitimate parts from malicious parts of the page, and consequently will parse and execute the whole page in the victim’s context.</p>
<p>For example, malicious HTML code can be injected via the innerHTML JavaScript method, usually used to render user-inserted HTML code. If strings are not correctly sanitized, the method can enable HTML injection. A JavaScript function that can be used for this purpose is document.write() .</p>
<p>Test Objectives: Identify HTML injection points and assess the severity of the injected content.</p>
<h4>Testing for Client-side URL Redirect</h4>
<p><b>ID: WSTG-CLNT-04</b></p>
<p>This section describes how to check for client-side URL redirection, also known as open redirection. It is an input validation flaw that exists when an application accepts user-controlled input that specifies a link which leads to an external URL that could be malicious. This kind of vulnerability could be used to accomplish a phishing attack or redirect a victim to an infection page. </p>

<h4>Testing for Client-side URL Redirect</h4>
<p><b>ID: WSTG-CLNT-04</b></p>
<p>It is also known as open redirection. It is an input validation flaw that exists when an application accepts user-controlled input that specifies a link which leads to an external URL that could be malicious. This kind of vulnerability could be used to accomplish a phishing attack or redirect a victim to an infection page. </p>
<p>This vulnerability occurs when an application accepts untrusted input that contains a URL value and does not sanitize it. This URL value could cause the web application to redirect the user to another page, such as a malicious page controlled by the attacker. </p>
<p>Objectives: Identify injection points that handle URLs or paths and assess the locations that the system could redirect to.</p>

<p>When testers manually check for this type of vulnerability, they first identify if there are client-side redirections implemented in the client-side code. These redirections may be implemented, to give a JavaScript example, using the window.location object. </p>
