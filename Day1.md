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
<p></p>


