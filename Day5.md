<h4>Testing for Vulnerable Remember Password</h4>
<p><b>ID: WSTG-ATHN-05</b></p>
<p>Many websites provide a remember me functionality. This helps the user to stay logged in for longer sessions. Objective here is to check wheather the generated session is managed securely and do not put the user's credentials in danger. They can be tested by: </p>
<ul>
	<li>Store the credentials in an encoded fashion in the browser’s storage mechanisms, which can be verified by following the web storage testing scenario and going through the session analysis scenarios.</li>
	<li>Automatically injcting user's credentials can be abused by: Clickjacking attacks and CSRF attacks.</li>
	<li>Tokens should be analyzed in terms of token-lifetime, where some tokens never expire and put the users in danger if those tokens ever get stolen.</li>
</ul>

<h4>Testing for Browser Cache Weaknesses</h4>
<p><b>ID: WSTG-ATHN-06</b></p>
<p>Browsers can store information for purposes of caching and history. Caching is used to improve performance, so that previously displayed information doesn’t need to be downloaded again. If sensitive information is displayed to the user (such as their address, credit card details, Social Security Number, or username),
then this information could be stored for purposes of caching or history, and therefore retrievable through examining the browser’s cache or by simply pressing the browser’s Back button. <br>Test Objectives:</p>
<ul>
	<li>Review if the application stores sensitive information on the client side.</li>
	<li>Review if the access can occur without authorization.</li>
</ul>
<ul>
	<li>Browser History: If by pressing the Back button the tester can access previous pages but not access new ones, then it is not an authentication issue, but a browser history issue. </li>
	<li>The Back button can be stopped from showing sensitive data. This can be done by: <br>
		Delivering the page over HTTPS. <br>
		Setting Cache-Control: must-revalidate</li>
	<li> For instance, if testers are testing an e-commerce application, they should look for all pages that contain a credit card number or some other financial information, and check that all those pages enforce the no-cache directive.</li>
	
</ul>

<h4>Testing for Weak Password Policy</h4>
<p><b>ID: WSTG-ATHN-07</b></p>
<p>The objective here is to Determine the resistance of the application against brute force password guessing using available password dictionaries by evaluating the length, complexity, reuse, and aging requirements of passwords. </p>

<h4>Testing for Weak Security Question Answer</h4>
<p><b>ID: WSTG-ATHN-08</b></p>
<p>Often called “secret” questions and answers, security questions and answers are often used to recover forgotten passwords. Sometimes the website lets user to generate its own set of questions and answers. They might be weak and can easily be bruteforced. Sometimes the questions created are absured.For eg, what is 1+1? and my password is s3curity.</p>

<p>How to test <br>If the website allows the user to choose an answer then choose the answer that is publicallly available. Determine how many guesses are possible. </p>

<h4>Testing for Weak Password Change or Reset Functionalities</h4>
<p><b>ID: WSTG-ATHN-09</b></p>
<p>The password change and reset function of an application is a self-service password change or reset mechanism for users. This self-service mechanism allows users to quickly change or reset their password without an administrator intervening. </p>
<p>How to test?</p>
<ul>
	<li>If users, other than administrators, can change or reset passwords for accounts other than their own.</li>
	<li>If users can manipulate or subvert the password change or reset process to change or reset the password of another user or administrator.</li>
	<li>If the password change or reset process is vulnerable to CSRF.</li>
</ul>

<p>Test Password Reset</p>
<ul>
	<li>What information is required to reset the password? Does it require secuirty questions or simply </li>
	<li>How are reset passwords communicated to the user? It would be insecure if the password reset tool shows you the password. A less insecure scenario is if the password reset tool forces the user to immediately change their password. The best scenario would be if the password reset is done via the email address. </li>
	<li>Is the reset password functionality requesting confirmation before changing the password? This could be generating an OPT and sending it to your email/phone. This is pretty helpful in case of Denail Of Service attacks.</li>
</ul>

<p>Test Password Change</p>
<p>Check if the password can be changed without requesting the new password.</p>

<h4>Testing for Weaker Authentication in Alternative Channel</h4>
<p><b>ID: WSTG-ATHN-10</b></p>
<p>Even if the primary authentication mechanisms do not include any vulnerabilities, it may be that vulnerabilities exist in alternative legitimate authentication user channels for the same user accounts.</p>
<p>The alternative user interaction channels could be utilized to circumvent the primary channel, or expose information that can then be used to assist an attack against the primary channel.</p>
<p>Some of these channels may themselves be separate web applications using different hostnames or paths. For example:</p>
<ul>
	<li>Standard website</li>
	<li>Mobile/specific value optimized website.</li>
	<li>Alternative country and language website.</li>
	<li>Parallel websites that utilize the same user accounts.</li>
	<li>Development, test, UAT and staging versions of the standard website</li>
</ul>

<h3>Authorization Testing</h3>
<h4>Testing Directory Traversal File Include</h4>
<p><b>WSTG-ATHZ-01</b></p>
<p>Many web applications use and manage files as part of their daily operation. Using input validation methods that have not been well designed or deployed, an aggressor could exploit the system in order to read or write files that are not intended to be accessible. In particular situations, it could be possible to execute arbitrary code or system commands.</p>

<h4>Testing for Bypassing Authorization Schema</h4>
<p><b>ID: WSTG-ATHZ-02</b></p>
<p>This test focusses how the authorization schema is implemented for each role or priviledge to get access to restriced pages/sections. </p>
<p>For every specific role the tester holds during the assessment and for every function and request that the application executes during the post-authentication phase, it is necessary to verify:</p>
<ul>
	<li>Is it possible to access that resource even if the user is not authenticated?</li>
	<li>Is it possible to access that resource after the log-out?</li>
	<li>Is it possible to access functions and resources that should be accessible to a user that holds a different role or privilege?</li>
</ul>
<p>Objective: Test if horizontal or vertical access is possible.</p>
<p>Supposet addUser is accesible to the admin after login. Try to request the page using /admin/addUser. Or if there is some other functionality then try to access it with your own cookies/session id but with the same paramters that the paga/functionality expects.</p>

<p><b>Special Headers: </b>Some applications support non-standard headers such as <b>X-Original-URL</b> or <b>X-Rewrite-URL</b> in order to allow overriding the target URL in requests with the one specified in the header value. This behavior can be leveraged in a situation in which the application is behind a component that applies access control restriction based on the request URL. </p>
<p>Send requests to non-existant pages using the special headers. If you get a response that the "resource existed was not found" or something similar than you can confirm that the web application supports special headers. You can then send requests to restriced pages using these special headers.</p>
<p>Other headers to consider</p>
<ul>
	<li>X-Forwarded-For</li>
	<li>X-Forward-For</li>
	<li>X-Remote-For</li>
	<li>X-Originating-IP</li>
	<li>X-Remote-Addr</li>
	<li>X-Client-IP</li>
</ul>
