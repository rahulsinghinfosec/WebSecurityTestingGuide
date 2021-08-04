<h4>Testing for CSRF</h4>
<p><b>ID: WSTG-SESS-05</b></p>
<p>Cross-Site Request Forgery (CSRF) is an attack that forces an end user to execute unintended actions on a web application in which they are currently authenticated. With a little social engineering, an attacker may force the users of a web application to execute actions of the attacker’s choosing. A successful
CSRF exploit can compromise end user data and operation when it targets a normal user.</p>
<p>Objective: Determine whether it is possible to initiate requests on a user’s behalf that are not initiated by the user.</p>

<h4>Testing For Logout Functionality</h4>
<p><b>ID: WSTG-SESS-06</b></p>
<p>Session termination is an important part of the session lifecycle. Reducing to a minimum the lifetime of the session tokens decreases the likelihood of a successful session hijacking attack. This can be seen as a control against preventing other attacks like Cross Site Scripting and Cross Site Request Forgery.</p>
<p>Such attacks have been known to rely on a user having an authenticated session present. Not having a secure session termination only increases the attack surface for any of these attacks.</p>
<p>A secure session termination requires at least the following components:</p>
<ul>
	<li>Availability of user interface controls that allow the user to manually log out.</li>
	<li>Session termination after a given amount of time without activity (session timeout).</li>
	<li>Proper invalidation of server-side session state.</li>
</ul>

<p>There are multiple issues which can prevent the effective termination of a session. For the ideal secure web
application, a user should be able to terminate at any time through the user interface. Every page should contain a log out button on a place where it is directly visible.</p>
<p>Another common mistake in session termination is that the client-side session token is set to a new value while the server-side state remains active and can be reused by setting the session cookie back to the previous value.</p>

<p>The usage of a single sign-on (SSO) system instead of an application-specific authentication scheme often causes the coexistence of multiple sessions which have to be terminated separately. For instance, the termination of the application-specific session does not terminate the session in the SSO system. Navigating back to the SSO portal offers the user the possibility to log back in to the application where the log out was performed just before. On the other side a log out function in a SSO system does not necessarily cause session termination in connected applications.</p>

<p>Test for server side session termination: Try to log out and see if the session id has been changed. If it has been changed then use the previous session id and see if you are logged in again.</p>

<p>Test for Single-Sign-On Environments (Single Sign-Off): Perform a log out in the tested application. Verify if there is a central portal or application directory which allows the user to log back in to the application without authentication. Test if the application requests the user to authenticate, if the URL of an entry point to the application is requested. While logged in in the tested application, perform a log out in the
SSO system. Then try to access an authenticated area of the tested application.</p>

<h4>Testing Session Timeout</h4>
<p><b>ID: WSTG-SESS-07</b></p>
<p>In this phase testers check that the application automatically logs out a user when that user has been idle for a certain amount of time, ensuring that it is not possible to “reuse” the same session and that no sensitive data remains stored in the browser cache.</p>
<p>If the application is idle or is inactive, it should automatically time out and discard the session. Hence logging out the user. For example, a 60 minute log out time for a public forum can be acceptable, but such a long time would be too much in a home banking application (where a maximum timeout of
15 minutes is recommended). </p>
<p>Session timeout management and expiration must be enforced server-side. If some data under the control of the client is used to enforce the session timeout, for example, a certain cookie value, or time (in cookie) for that matter. This can be easily manipulated by the users. Hence, session management and expirations must be enforeced on the server side.</p>
<p>More specifically, as for the log out function, it is important to ensure that all session tokens (e.g. cookies) are properly destroyed or made unusable, and that proper controls are enforced server-side to prevent the reuse of session tokens.</p>
<p>If the user logs out, the session token must be destroyed and proper controls must be made on the servers side to prevent the reuse of session tokens.</p>
<p>Objective: Validate that a hard session timeout exists.</p>
<p>Methodology:<br>First, testers have to check whether a timeout exists, for instance, by logging in and waiting for the timeout log out to be triggered.<br>Then, if the timeout is configured, testers need to understand whether the timeout is enforced by the client or by the server (or both). Testers could try to modify the cookie (if it’s not cryptographically protected) and see what happens to the session. For instance, testers can set the cookie expiration date far in the future and see whether the session can be prolonged.</p>

<h4>Testing for Session Puzzling</h4>
<p><b>ID: WSTG-SESS-08</b></p>
<p>Session Variable Overloading (also known as Session Puzzling) is an application level vulnerability which can enable an attacker to perform a variety of malicious actions. This includes : </p>

<ul>
	<li>Bypass efficient authentication enforcement mechanisms, and impersonate legitimate users.</li>
	<li>Elevate the privileges of a malicious user account, in an environment that would otherwise be considered foolproof.</li>
	<li>Skip over qualifying phases in multi-phase processes, even if the process includes all the commonly recommended code level restrictions.</li>
	<li>Manipulate server-side values in indirect methods that cannot be predicted or detected.</li>
	<li>Execute traditional attacks in locations that were previously unreachable, or even considered secure.</li>
</ul>

<p>This vulnerability occurs when an application uses the same session variable for more than one purpose. An attacker can potentially access pages in an order unanticipated by the developers so that the session variable is set in one context and then used in another. </p>

<p>For example, an attacker could use session variable overloading to bypass authentication enforcement mechanisms of applications that enforce authentication by validating the existence of session variables that contain identity–related values, which are usually stored in the session after a successful authentication process. This means an attacker first accesses a location in the application that sets session context and then accesses privileged locations that examine this context.</p>

<p>Objectives: Identify all session variables. <br> Break the logical flow of session generation.</p>
