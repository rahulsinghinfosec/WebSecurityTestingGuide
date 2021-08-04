<h4>Testinf for XPath Injection</h4>
<p><b>ID: WSTG-INPV-09</b></p>
<p>XPath is a language that has been designed and developed primarily to address parts of an XML document. In XPath injection testing, we test if it is possible to inject XPath syntax into a request interpreted by the application, allowing an attacker to execute user-controlled XPath queries. When successfully exploited, this vulnerability may allow an attacker to bypass authentication mechanisms or access information without proper authorization.</p>
<p>There are different kinds of databases. Though SQL databases are quite common and more likely to be found, there are databses that store data in XML format rather than a table format. XML databases uses XPath as their query language.</p>

<p>From a conceptual point of view, XPath is very similar to SQL in its purpose and applications, an interesting result is that XPath injection attacks follow the same logic as SQL Injection attacks.Another
advantage of an XPath injection attack is that, unlike SQL, no ACLs are enforced, as our query can access every part of the XML document.</p>

<h4>Testing for IMAP and SMTP Injection</h4>
<p><b>ID: WSTG-INPV-10</b></p>
<p>This threat affects all applications that communicate with mail servers (IMAP/SMTP), generally webmail applications. The aim of this test is to verify the capacity to inject arbitrary IMAP/SMTP commands into the mail servers, due to input data not being properly sanitized. </p>
<p>An IMAP/SMTP Injection makes it possible to access a mail server which otherwise would not be directly accessible from the Internet. In some cases, these internal systems do not have the same level of infrastructure security and hardening that is applied to the front-end web servers. Therefore, mail server results may be more vulnerable to attacks by end users. </p>
<p>It is important to note that the requests being sent should match the technology being tested. Sending SQL injection strings for Microsoft SQL server when a MySQL server is being used will result in false positive responses. In this case, sending malicious IMAP commands is modus operandi since IMAP is the underlying protocol being tested.</p>
<p>For example : http://&lt;webmail&gt;/src/read_body.php?mailbox=INBOX&passed_id=46106&startMessage=1<br>Try to manipulate and emilinate the paramaters. Try adding a Comma(") and other special characters to check if the application throws an error. Try to change the paramater value and then add or remove any paramater. Any change compared against the original (untampered) request ensures that the application is vulnerable to IMAP/SMTP injection. </p>

<h4>Testing for Code Injection</h4>
<p><b>ID: WSTG-INPV-11</b></p>
<p>In Code Injection testing, a tester submits input that is processed by the web server as dynamic code or as an included file. These tests can target various server-side scripting engines, e.g., ASP or PHP. Proper input validation and secure coding practices need to be employed to protect against these attacks.</p>

<h5>Testing for Local File Inclusion</h5>
<p>The File Inclusion vulnerability allows an attacker to include a file, usually exploiting a “dynamic file inclusion” mechanisms implemented in the target application. The vulnerability occurs due to the use of user-supplied input without proper validation. Depending upon the severity it can also lead to:</p>
<ul>
	<li>Code Execution</li>
	<li>Dos</li>
	<li>Information Disclosure</li>
</ul>
<p>Consider the code: &tl;?php include($_GET['file'].".php"); ?&gt;. ".php" will be appended to the name of the file provided. This can be bypassed by</p>
<ul>
	<li>Null byte injection. This is not possible in PHP versions > 5.3</li>
	<li>Path and Dot Truncation. Most PHP installations have filelimit of 4096 bytes. Entering a name of length of greater than 4096 bytes, simply discards the additional characters.</li>
	<li>PHP Wrappers. In some specific implementations this vulnerability can be used to upgrade the attack from LFI to Remote Code Execution vulnerabilities that could potentially fully compromise the host. A wrapper is a code that surrounds other code to perform some added functionality. PHP implements many built-in wrappers to be used with file system functions.</li>
	<ul>
		<li>PHP Filter</li>
		<li>PHP ZIP</li>
		<li>PHP Data</li>
		<li>PHP Expect: Not enabled by default, provides access to strerr, stdin, stdout.</li>
	</ul>
</ul>

<h5>Testing for Remote File Inclusion</h5>
<p>Remote File Inclusion (also known as RFI) is the process of including remote files through the exploiting of vulnerable inclusion procedures implemented in the application. This vulnerability occurs, for example, when a page receives, as input, the path to the file that has to be included and this input is not properly sanitized, allowing external URL to be injected.</p>

<h4>Testing for Command Injection</h4>
<p><b>ID: WSTG-INPV-12</b></p>
<p>OS command injection is a technique used via a web interface in order to execute OS commands on a web server. The user supplies operating system commands through a web interface in order to execute OS commands.</p>
<p>When viewing a file in a web application, the filename is often shown in the URL. Perl allows piping data from a process into an open statement. The user can simply append the Pipe symbol <code>|</code> onto the end of the filename. <br>Example URL : <code>http://sensitive/cgi-bin/userData.pl?doc=user1.txt</code><br>Example URL modified: <code>http://sensitive/cgi-bin/userData.pl?doc=/bin/ls|</code>.<br>You can also try to add semicolons, amperand, etc.</p>

<p>Code Review Dangerous APIs</p>
<ul>
	<li>Java: <code>Runtime.exec()</code></li>
	<li>C/C++: system, exec, shellExecute</li>
	<li>Python: </li>
	<ul>
		<li>exec</li>
		<li>eval</li>
		<li>os.system</li>
		<li>subprocess.popen</li>
		<li>subprocess.call</li>
	</ul>
	<li>PHP</li>
	<ul>
		<li>system</li>
		<li>exec</li>
		<li>shell_exec</li>
		<li>proc_open</li>
		<li>eval</li>
	</ul>
</ul>

<h4>Testing for Buffer Overflow</h4>
<p><b>ID: WSTG-INPV-13</b></p>
<p>Check for Buffer Overflows, interger overflows,etc. </p>
