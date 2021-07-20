<h3>Configuration and Deployment Management Testing</h3>
<h4>Test Network Infrastructure Configuration</h4>
<p>ID: WSTG-CONF-01</p>
<p>Need to check for miscofingurations or vulnerabilities in the server or the infrastructure itself. This could be testing for <b>Known Server Vulneratbilities</b>, <b>Administrative Tools</b>, etc.</p>

<h4>Test Applicatoin Platform Configuration</h4>
<p><b>ID: WSTG-CONF-02</b></p>
<p>Its important that each individual element is properly configured to meet your needs and in terms of security.Ensure that defaults and known files have been removed. Validate that no debugging code or extensions are left in the production environments. Review the logging mechanisms set in place for the application.</p>
<p>Look for comments,log files, remove default error pages, change Log storage, etc.</p>

<h4>Test File Extensions Handling for Sensitive Information</h4>
<p><b>ID: WSTG-CONF-03</b></p>
<p>File extensions are commonly used in web servers to easily determine which technologies, languages and plugins
must be used to fulfill the web request. They can help pen-testers understand the underlying technology and mis-configuration of web servers could easily reveal confidential information about access credentials.</p>
<p>Extension checking is often used to validate files to be uploaded, which can lead to unexpected results because the
content is not what is expected, or because of unexpected OS filename handling.</p>
<p>Determining how web servers handle requests corresponding to files having different extensions may help in
understanding web server behavior depending on the kind of files that are accessed. For example, it can help to
understand which file extensions are returned as text or plain versus those that cause server-side execution. The latter
are indicative of technologies, languages or plugins that are used by web servers or application servers, and may
provide additional insight on how the web application is engineered.</p>
<p>Can be tested using : Forced browsing(submitting requests with different extensions)<br> You can check for the following extensions.</p>
<ul>
  <li>.zip, .tar, .gz, .tgz, .rar, etc. (compresses files)</li>
  <li>.java</li>
  <li>.txt, .asa, .inc, .config, etc</li>
  <li>.pdf, .docx , .rtf , .xlsx , .pptx , etc.</li>
  <li>.bak, .old, ~ , other backup extensions.</li>
</ul>

<h4>Review Old Backup and Unreferenced Files for Sensitive Information</h4>
<p><b>ID: WSTG-CONF-04</b></p>
<p>It isn’t uncommon to find unreferenced or forgotten files that can be used to obtain important information about the infrastructure or the credentials. Most common scenarios include the presence of renamed old versions of modified files, inclusion files that are loaded
into the language of choice and can be downloaded as source, or even automatic or manual backups in form of compressed archives. Backup files can also be generated automatically by the underlying file system the application is
hosted on, a feature usually referred to as “snapshots”.</p>
<p>You can look into the robots.txt file, bruteforce, blind guess(based on your knowlege of the application),Use of publically available information(search engines might have crawled the website before), waybackurls, </p>
