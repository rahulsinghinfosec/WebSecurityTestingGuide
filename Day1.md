<h1>OWASP Testing Methodology</h1>
<p>It is based on <b>Black Box</b> approach. Security testing is only an appropriate technique for testing the security of web applications under
certain circumstances. The goal of OWASP Web Security Testing Guide is to collect all the possible testing techniques, explain these techniques,
and keep the guide updated.</p>
<p>The testing model consists of</p>
<ul>
  <li>Tester</li>
  <li>Tools and Methodology</li>
  <li>Application (to Pen-test)</li>
</ul>

<h1>Types of Testing</h1>
<p>Testing can be categorised as <b>Passiv</b> and <b>Active</b></p>
<h2>Passive Testing</h2>
<p>In Passive testing, the tester understands the logic and the flow of the application. Makes himself aware of all the functionalities,etc. 
This phase is concerned with gatering as much information as possible. This could include Server name & version, headers, access points, etc.</p>
<h2>Active Testing</h2>
<p>OWASP has divided this into 12 parts/sections (with a name/titile assigned to each section and its subsections)</p>
<ol>
  <li>Information Gathering</li>
  <li>Configuration and Deployment Management Testing</li>
  <li>Identity Management Testing</li>
  <li>Authentication Testing</li>
  <li>Authorization Testing</li>
  <li>Session Management Testing</li>
  <li>Input Validation Testing</li>
  <li>Error Handling</li>
  <li>Cryptography</li>
  <li>Business Logic Testing</li>
  <li>Client Side Testing</li>
  <li>API Testing</li>
</ol>

<h2>Information Gathering</h2>
<p>It is further divided into: </p>
<ol>
  <li>Conduct Search Engine Discovery Reconnaissance for Information Leakage</li>
  <li>Fingerprinting Web Server</li>
  <li>Review Webserver Metafiles for Information Leakage</li>
  <li>Enumerate Applications on Webserver</li>
  <li>Review Webpage Content for Information Leakage</li>
  <li>Identify Application Entry Points</li>
  <li>Map Execution Paths Through Application</li>
  <li>Fingerprint Web Application Framework</li>
  <li>Map Application Architecture</li>
</ol>
<h4>Conduct Search Engine Discovery Reconnaissance for Information Leakage</h4>
<p><b>ID: WSTG-INFO-01</b></p>
<p>You can leverage the power of search engines to look for sensitve files, which might not be intented for the public to view but the crawler might have scanned it.
  You can use search engines like: <b>Google, Bing, DuckDuckGo, Internet Archive (Wayback Machine), Shodan, binsearch.info, Common crawl,etc.</b></p>
<p>You can make use of search operators like : <b>site, intitle,cache,inbody,etc.</b> <a href="https://www.exploit-db.com/google-hacking-database">Google Hacking Database</a> 
  is a useful resource to uncover specific information. <br> <a href="https://resources.bishopfox.com/resources/tools/google-hacking-diggity/">Google Hacking Diggity Project.</a></p>

<h4>Fingerpring Web Server</h4>
<p><b>ID : WSTG-INFO-02</b></p>
<p>This involves finding the type and version of the web server. This can help to narrow down your search for vuln assessments and thus exploitation.
  This generally involves grabbing the banner of the header information from the web response. Admins often obfuscate their banners or response headers to prevent exposing their web application servers.
  Hence manual testing is performed with different techniques. This could involve looking at the errors returned, or looking at the sequence of the headers, or even some web applicaiton server specific headers.
  Now-a-days automated scanners <b>(like nikto, netcraft, nmap,etc.)</b> are present which can do it for the testers. They use the same mehtodology to find the server, and are good enough to not be fooled by obfuscated banners.But nevertheless, manual testing should be performed.
</p>
<h4>Review Webserver Metafiles for Information Leakage</h4>
<p><b>ID: WSTG-INFO-03</b></p>
<p>Many-a-times, you can gather a lot of information about the application by viewing the metafiles. These files are sometimes accessible from the home directory, 
but can ofthen be hidden (for obvious reasons).<br>
They include</p>
<ul>
  <li>robots.txt</li>
  <li>META tags</li>
  <li>sitemap (sitemap.xml)</li>
  <li>security.txt : allows websites to define security standards, and contact details.</li>
  <li>humans.txt</li>
  <li>There are other RFCs and Internet Drafts which suggest standardized uses of files within the <b>.well-known/</b> directory. So you can look into this directory as well.</li>
</ul>
<h4>Enumerate Applications on Webserver</h4>
<p><b>ID: WSTG-INFO-04</b></p>
<p>Different environments run different web applications. Before the tester proceeds further, its important to know the testing web application.It may be possible that different web applications might be running on the same IP address</p>
<ul>
  <li>Different Based URL: Example : http://ip/url1, http://ip/url2, http://ip/url3 might be running 3 different web applications altogether.</li>
  <li>Non-Standard Port Numbers: It is often possible that the web application might be running on a different port, which might not be provided to you.</li>
  <li>Virtual Hosts: There might be subdomains to the web application running different web application altogether.</li>
</ul>
<h4>Review Webpage Content For Information Leakage</h4>
<p><b>ID: WSTG-INFO-05</b></p>
<p>It is common for web app developers to write comments on the web page, but it could also reveal some sensitive information. New frameworks like ReactJS, AngularJS might, etc. might make it difficult to read the source code, but still there are ways around that.</p>
<p>Look for robots.txt files, META tags, comments, script tags (Try to find API Keys, hardcoded varibles; it also helps you understand the application better), source map files. For example a tester sees: <b>/static/js/main.chunk.js</b>, he can add <b>.map</b> at the end, thus making it <b>/static/js/main.chunk.js.map</b>. Source map files may reveal some sensitive infomation.</p>
<h4>Identify Application Entry Points</h4>
<p><b>ID: WSTG-INFO-06</b></p>
<p>It is important to know the web application and the attack surface, to know what you are dealing with and what can you do to exploit it. A good knowledge of request methods, headers, etc might be helpful. Here you look for url paramaters, headers, cookies set, redirects, forbidden pages/directories, etc.</p>
<p>Tool : OWASP Attack Surface Detector</p>

<h4>Map Execution Paths through Application</h4>
<p>ID: WSTG-INFO-07</p>
<p>Methods: Code Review, Automated Spidering </p>

<h4>Fingerprint Web Application Framework</h4>
<p><b><ID: WSTG-INFO-08/b></p>
<p>Knowing the web application components that are being tested significantly helps in the testing process and will also drastically reduce the effort required during the test.There are a couple of things that can help you identify the framework.</p>
<ul>
	<li>HTTP Headers : You may look for special headers that may be pointing to the Framework being used. Headers like, <b>X-Powered-By, X-Generator</b>.They are often obfuscated.</li>
	<li>Cookies : This is a bit more reliable than the previous approach. There are framework specific cookies that can help you identify the framework.</li>
	<li>HTML Source Code : Look for framework specific paths, files, and even comments written can help.</li>
	<li>Specific Files and Folders : Try bruteforcing and looking in robots.txt file.</li>
	<li>File Extensions</li>
</ul>
<p>Tools : WhatWeb, Wappalyzer</p>

<h4>Fingerprint Web Application</h4>
<p><b>ID: WSTG-INFO-09</b></p>
<p>This is merged into <b>Fingerprint Web APplication Framework</b></p>

<h4>Map Application Architecture</h4>
<p><b>ID: WSTG-INFO-10</b></p>
<p>The application architecture needs to be mapped through some test to determine what different components are used to build the web application.In small setups, such as a simple PHP application, a single server might be used that serves the PHP application, and perhaps also the authentication mechanism.</p>

<p>On more complex setups, such as an online bank system, multiple servers might be involved. These may include a reverse proxy, a front-end web server, an application server, and a database server or LDAP server. Each of these servers will be used for different purposes and might even be segregated in different networks with firewalls between them. Sometimes there will be reverse proxies and you can identify them using thier headers. </p>
