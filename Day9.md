<h5>Testing for orcale</h5>
<p>Web based PL/SQL applications are enabled by the PL/SQL Gateway, which is is the component that translates web requests into database queries. Oracle has developed a number of software implementations, ranging from the early web listener product to the Apache mod_plsql module to the XML Database (XDB) web server.</p>
<p>Web server takes a web request and then, decides if it should be processed by the PL/SQL gateway. The PL/SQL Gateway processes the request by extracting the requested package name, procedure, and variables. This then sends it to the database server and the database server returns the response as html.</p>
<p>So, if the PL/SQL was exploited, no firewall would block are request and the entire web server would get exploited. </p>
<p>URLs for PL/SQL are easily recognizable and generally start with (xyz, etc.)</p>
<ul>
	<li>http://www.example.com/pls/xyz</li>
	<li>http://www.example.com/xyz/owa</li>
	<li>http://www.example.com/xyz/plsql</li>
</ul>
<p>In the plsql.conf Apache configuration file, /pls is the default, specified as a Location with the PLS module as the handler. The location need not be /pls, however. If in the following URL <b>http://www.server.com/aaa/bbb/xxxxx.yyyyy</b>, if xxxxx.yyyyy is replaced with ebank.home , store.welcome , auth.login , or
books.search, etc. then there is a strong chance that PL/SQL is being used.</p>
<p>For more detials on how to exploit and confirm the presence of PL/SQL refer to OWASP WSTG 4.2 (or higher) or some online resource.</p>
<p>Similarly, finger print the database first. This will help you to narrow down the payloads and tell you a lot about the attack surface.</p>
<p>Depending upon the database, different payloads can be used.</p>
<ul>
	<li>MYSQL</li>
	<li>MSSQL</li>
	<li>PostgreSQL</li>
	<li>Oracle </li>
	<li>MS ACCESS,NoSQL, etc.</li>
	<li>Testing for ORM Injection</li>
</ul>
<h5>Testing for ORM Injection</h5>
<p>Object Relational Mapping (ORM) Injection is an attack using SQL Injection against an ORM generated data access object model. From the point of view of a tester, this attack is virtually identical to a SQL Injection attack. However, the injection vulnerability exists in code generated by the ORM layer. </p>
<p>The benefits of using an ORM tool include quick generation of an object layer to communicate to a relational database, standardize code templates for these objects, and that they usually provide a set of safe functions to protect against SQL Injection attacks. </p>
<p>The benefits of using an ORM tool include quick generation of an object layer to communicate to a relational database, standardize code templates for these objects, and that they usually provide a set of safe functions to protect against SQL Injection attacks. </p>
<p>It is possible, however, for a web application using ORM generated objects to be vulnerable to SQL Injection attacks if methods can accept unsanitized input parameters.</p>

<h4>Testing for LDAP Injection</h4>
<p><b>ID: WSTG-INPV-06</b></p>
<p>The Lightweight Directory Access Protocol (LDAP) is used to store information about users, hosts, and many other objects. LDAP injection is a server-side attack, which could allow sensitive information about users and hosts represented in an LDAP structure to be disclosed, modified, or inserted. This is done by manipulating input parameters afterwards passed to internal search, add, and modify functions. </p>
<p>A web application could use LDAP in order to let users authenticate or search other users??? information inside a corporate structure. The goal of LDAP injection attacks is to inject LDAP search filters metacharacters in a query which will be executed by the application.</p>
<p>An LDAP search filter is constructed in Polish notation, also known as Polish notation prefix notation.</p>
<p>This means a pseudo code condition like this: </p>
<code>find("cn=John & userPassword=mypass") will be represented as: find("(&(cn=John)(userPassword=mypass))")</code>
<p>A successful exploitation of an LDAP injection vulnerability could allow the tester to:</p>
<ul>
	<li>Access unauthorized content</li>
	<li>Evade application restrictions</li>
	<li>Gather unauthorized informations</li>
	<li>Add or modify Objects inside LDAP tree structure.</li>
</ul>

<h4>Testing for XML Injection</h4>
<p><b>ID: WSTG-INPV-07</b></p>
<p>XML Injection testing is when a tester tries to inject an XML doc to the application. If the XML parser fails to contextually validate data, then the test will yield a positive result.</p>
<p>CDATA can be leveraged to perform an XSS attack, if XML document is processed to generate an HTML tag. </p>
<p>The following Java APIs might be vulnerable to XXE if they aren't configured properly.</p>
<p>
	javax.xml.parsers.DocumentBuilder <br>
javax.xml.parsers.DocumentBuildFactory <br>
org.xml.sax.EntityResolver <br>
org.dom4j.* <br>
javax.xml.parsers.SAXParser <br>
javax.xml.parsers.SAXParserFactory <br>
TransformerFactory <br>
SAXReader <br>
DocumentHelper <br>
SAXBuilder <br>
SAXParserFactory <br>
XMLReaderFactory <br>
XMLInputFactory <br>
SchemaFactory <br>
DocumentBuilderFactoryImpl <br>
SAXTransformerFactory <br>
DocumentBuilderFactoryImpl <br>
XMLReader <br>
Xerces: DOMParser, DOMParserImpl, SAXParser, XMLParser <br>
Java POI office</p>
<h4> Testing for SSI Injection </h4>
<p><b>ID: WSTG-INPV-08</b></p>
<p>Web servers usually give developers the ability to add small pieces of dynamic code inside static HTML pages, without having to deal with full-fledged server-side or client-side languages. This feature is provided by Server-Side Includes(SSI). </p>
<p>Server-Side Includes are directives that the web server parses before serving the page to the user. They represent an alternative to writing CGI programs or embedding code using server-side scripting languages, when there???s only need to perform very simple tasks. </p>
<p>Another way of verifying that SSI directives are enabled is by checking for pages with the .shtml extension, which is associated with SSI directives. The use of the .shtml extension is not mandatory, so not having found any .shtml files doesn???t necessarily mean that the target is not vulnerable to SSI injection attacks.</p>
