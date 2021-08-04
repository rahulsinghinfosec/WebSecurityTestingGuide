<h4>Test Cloud Storage</h4>
<p><b>ID: WSTG-CONF-11</b></p>
<p> Cloud storage services facilitate web application and services to store and access objects in the storage service. Improper access control configuration, however, may result in sensitive information exposure, data being tampered, or unauthorized access. </p>
<p>A known example is where an Amazon S3 bucket is misconfigured, although the other cloud storage services may also be exposed to similar risks. By default, all S3 buckets are private and can be accessed only by users that are explicitly granted access. Users can grant public access to both the bucket itself and to individual objects stored within that bucket. This may lead to an unauthorized user being able to upload new files, modify or read stored files.</p>

<h3>Identify Management Testing</h3>
<h4>Test Role Definitions</h4>
<p><b>ID: WSTG-IDNT-01</b></p>
<p>Applications have different types of functionalities and services, and those require access permissions based on the roles of the user.</p>
<p>This could be : an administrator, an auditor, a support enginner, a customer.<br>You need to:</p>
<ul>
	<li>Identify and document roles used by the application.</li>
	<li>Attempt to switch, change, or access another role.</li>
	<li>Review the granularity of the roles and the needs behind the permissions given.</li>
</ul>
<p>Methodology: Identify proper roles, switch to available roles, review roles permissions, etc. </p>

<h4>Test User Registration Process</h4>
<p><b>ID: WSTG-IDNT-02</b></p>
<p>Some websites offer a user registration process that automates (or semi-automates) the provisioning of system access to users.Test Objectives:</p>
<ul>
	<li>Verify that the identity requirements for user registration are aligned with business and security requirements.</li>
	<li>Validate the registration process.</li>
</ul>

<h4>Test Account Provisioning Process</h4>
<p><b>ID: WSTG-IDNT-03</b></p>
<p>The provisioning of accounts presents an opportunity for an attacker to create a valid account without application of the proper identification and authorization process.<br>Objectives: Verify which accounts may provision other accounts and of what type.</p>

<h4>Testing for User Enumeration and Guessable User Account</h4>
<p><b>
	ID: WSTG-IDNT-04
</b></p>
<p>The scope of this test is to verify if it is possible to collect a set of valid usernames by interacting with the authentication mechanism of the application. This test will be useful for brute force testing, in which the tester verifies if, given a valid username, it is possible to find the corresponding password.</p>

<h4>Testing for Weak or Unenforced Username Policy</h4>
<p><b>ID: WSTG-IDNT-05</b></p>
<p>User account names are often highly structured and valid account names can easily be guessed.
<br>Objectives:</p>
<ul>
	<li>Determine whether a consistent account name structure renders the application vulnerable to account
enumeration.</li>
	<li>Determine whether the application’s error messages permit account enumeration.</li>
</ul>

<h3>Authentication Testing</h3>
<h4>Testing for Credentials Transported over an Encrypted Channel</h4>
<p><b>ID: WSTG-ATHN-01</b></p>
<p>Testing for credentials transport verifies that web applications encrypt authentication data in transit. This encryption prevents attackers from taking over accounts by sniffing network traffic.Web applications use HTTPS to encrypt information in transit for both client to server and server to client communications.</p>
<p>The fact that traffic is encrypted does not necessarily mean that it’s completely safe. The security also depends on the encryption algorithm used and the robustness of the keys that the application is using.</p>
<p>Methodology</p>
<p>Find the address of the login page and attempt to switch the protocol to HTTP. For example, the URL for the forced browsing could look like the following: http://www.example.org/login.If the login page is normally HTTPS, attempt to remove the “S” to see if the login page loads as HTTP.Log in using a valid account while attempting to force the use of unencrypted HTTP. In a passing test, the login request
should be HTTPS</p>

<h4>Testing for Default Credentials</h4>
<p><b>ID: WSTG-ATHN-02</b></p>
<p>Nowadays web applications often make use of popular Open Source or commercial software that can be installed on servers with minimal configuration or customization by the server administrator.Moreover, a lot of hardware appliances (i.e. network routers and database servers) offer web-based configuration or administrative interfaces.</p>

<p>Often these applications, once installed, are not properly configured and the default credentials provided for initial authentication and configuration are never changed. These default credentials are well known by penetration testers and, unfortunately, also by malicious attackers, who can use them to gain access to various types of applications.</p>

<p>When you have identified an application interface, for example a Cisco router web interface or a WebLogic
administrator portal, check that the known usernames and passwords for these devices do not result in successful authentication. To do this you can consult the manufacturer’s documentation or, in a much simpler way, you can find common credentials using a search engine or by using one of the sites or tools listed in the Reference section.</p>

<h4>Testing for Weak Lock Out Mechanism</h4>
<p><b>ID: WSTG-ATHN-03</b></p>
<p>Account lockout mechanisms are used to mitigate brute force attacks. Some of the attacks that can be defeated by using lockout mechanism:</p>
<ul>
	<li>Login password or username guessing attack.</li>
	<li>Code guessing on any 2FA functionality or Security Questions.</li>
</ul>
<p>Account lockout mechanisms require a balance between protecting accounts from unauthorized access and protecting users from being denied authorized access. Accounts are typically locked after 3 to 5 unsuccessful attempts and can only be unlocked after a predetermined period of time, via a self-service unlock mechanism, or intervention by an administrator.</p>
<p>Despite it being easy to conduct brute force attacks, the result of a successful attack is dangerous as the attacker will have full access on the user account and with it all the functionality and services they have access to. <br>Objectives:</p>
<ul>
	<li>Evaluate the account lockout mechanism’s ability to mitigate brute force password guessing.</li>
	<li>Evaluate the unlock mechanism’s resistance to unauthorized account unlocking.</li>
</ul>

<p>
	If there's a CAPTCHA, try to bypass it. CAPTCHA has its own set of weaknesses, if not implemented properly.
	There could an an ALT attribute. Try to bruteforce CAPTCHA, or even inject values, or even try to submit requests without CAPTCHA.
</p>

<h4>Testing for Bypassing Authentication Schema</h4>
<p><b>ID: WSTG-ATHN-04</b></p>
<p>Testing the authentication schema means understanding how the authentication process works and using that information to circumvent the authentication mechanism. In addition, it is often possible to bypass authentication measures by tampering with requests and tricking the application into thinking that the user is already authenticated. This can be accomplished either by modifying the given URL parameter, by manipulating the form, or by counterfeiting sessions.</p>

<p>This can be accomplished using : </p>
<ul>
	<li>Direct page request(forced browsing). Check for pages that do not require authentication and can be bypassed without requiring credentials.</li>
	<li>Paramater Modification</li>
	<li>Session ID Prediction</li>
	<li>SQL or NoSQL Injectoin</li>
</ul>
