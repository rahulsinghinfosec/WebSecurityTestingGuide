<h4>Testing for Padding Oracle</h4>
<p><b>ID: WSTG-CRYP-02</b></p>
<p>A padding oracle is a function of an application which decrypts encrypted data provided by the client, e.g. internal session state stored on the client, and leaks the state of the validity of the padding after decryption. The existence of a padding oracle allows an attacker to decrypt encrypted data and encrypt arbitrary data without knowledge of the key used for these cryptographic operations.</p>
<p>Block ciphers encrypt data only in blocks of certain sizes. Block sizes used by common ciphers are 8 and 16 bytes. Data where the size doesn’t match a multiple of the block size of the used cipher has to be padded in a specific manner so the decryptor is able to strip the padding. A commonly used padding scheme is PKCS#7. It fills the remaining bytes with the value of the padding length. If the padding has the length of 5 bytes, the byte value 0x05 is repeated five times after the plain text. A padding oracle is present if an application leaks this specific padding error condition for encrypted data provided by the client. Certain modes of operation of cryptography allow bit-flipping attacks, where flipping of a bit in the cipher text causes
that the bit is also flipped in the plain text. </p>
<p>The padding oracle attack enables an attacker to decrypt encrypted data without knowledge of the encryption key and used cipher by sending skillful manipulated cipher texts to the padding oracle and observing of the results returned by it. This causes loss of confidentiality of the encrypted data. </p>
<p>A padding oracle attack also enables an attacker to encrypt arbitrary plain texts without knowledge of the used key and cipher. </p>

<h4>Testing for Sensitive Information Sent via Unencrypted Channels</h4>
<p><b>ID: WSTG-CRYP-03</b></p>
<p>Sensitive data must be protected when it is transmitted through the network. If data is transmitted over HTTPS or encrypted in another way the protection mechanism must not have limitations or vulnerabilities. </p>
<p>As a rule of thumb if data must be protected when it is stored, this data must also be protected during transmission. Some examples for sensitive data are: </p>
<ul>
	<li>Information used in authentication</li>
	<li>Information protected by laws, regulations or specific organizational policy (e.g. Credit Cards, Customers data)</li>
</ul>
<p>A typical example is the usage of Basic Authentication over HTTP. When using Basic Authentication, user credentials are encoded rather than encrypted, and are sent as HTTP headers.</p>
<p>Another typical example is authentication forms which transmit user authentication credentials over HTTP. If you can see HTTP being used in the action attribute of the form, then credentials will be sent as plaintext. It is also possible to see this issue by examining the HTTP traffic with an interception proxy.</p>
<p>The Session ID Cookie must be transmitted over protected channels. If the cookie does not have the secure flag set, it is permitted for the application to transmit it unencrypted. </p>
<p>Test for passwords or hardcoded strings in the source code of the website. <br><code>grep -r –E
"Pass | password | pwd |user | guest| admin | encry | key | decrypt | sharekey " ./PathToSearch/</code> <br>
<code>grep -r " {2\}[0-9]\{6\} " ./PathToSearch/</code></p>

<h4>Testing for Weak Encryption</h4>
<p><b>ID: WSTG-CRYP-04</b></p>
<p>Incorrect uses of encryption algorithms may result in sensitive data exposure, key leakage, broken authentication, insecure session, and spoofing attacks. There are some encryption or hash algorithms known to be weak and are not suggested for use such as MD5 and RC4. In addition to the right choices of secure encryption or hash algorithms, the right uses of parameters also matter for the security level. For example, ECB (Electronic Code Book) mode is not suggested for use in asymmetric encryption.</p>
<p><b>Basic Security Checklist</b></p>
<ul>
	<li>When using AES128 or AES256, the IV (Initialization Vector) must be random and unpredictable.For
        example, in Java, java.util.Random is considered a weakrandom number  generator. java.security.SecureRandom should be used instead of java.util.Random .</li>
	<li>For asymmetric encryption, use Elliptic Curve Cryptography (ECC) with a secure curve like Curve25519 preferred. If ECC can’t be used then use RSA encryption with a minimum 2048bit key.</li>
	<li>When uses of RSA in signature, PSS padding is recommended.</li>
	<li>Weak hash/encryption algorithms should not be used such MD5, RC4, DES, Blowfish, SHA1. 1024-bit RSA or
DSA, 160-bit ECDSA (elliptic curves), 80/112-bit 2TDEA (two key triple DES)</li>
	<li>When symmetric encryption algorithm is used, ECB (Electronic Code Book) mode should not be used.</li>
	<li>When PBKDF2 is used to hash password, the parameter of iteration is recommended to be over 10000.</li>
</ul>


<h5>Business Logic Testing</h5>
<p>Testing for business logic flaws in a multi-functional dynamic web application requires thinking in unconventional methods. If an application’s authentication mechanism is developed with the intention of performing steps 1, 2, 3 in that specific order to authenticate a user. What happens if the user goes from step 1 straight to step 3? In this simplistic example, does the application provide access by failing open; deny access, or just error out with a 500 message?</p>
<h4>Test Business Logic Data Validation</h4>
<p><b>ID: WSTG-BUSL-01</b></p>
<p>The application must ensure that only logically valid data can be entered at the front end as well as directly to the server-side of an application of system. Only verifying data locally may leave applications vulnerable to server injections through proxies or at handoffs with other systems. This is different from simply performing Boundary Value Analysis (BVA) in that it is more difficult and in most cases cannot be simply verified at the entry point, but usually requires checking some other system.</p>
<p>Test Objectives: Identify data injection points, Validate that all checks are occurring on the back end and can’t be bypassed, Attempt to break the format of the expected data and analyze how the application is handling it.</p>
<h4>Test Ability to Forge Requests</h4>
<p><b>ID: WSTG-BUSL-02</b></p>
<p>Forging requests is a method that attackers use to circumvent the front end GUI application to directly submit information for back end processing. The goal of the attacker is to send HTTP POST/GET requests through an intercepting proxy with data values that is not supported, guarded against or expected by the applications business logic. Some examples of forged requests include exploiting guessable or predictable parameters or expose “hidden” features and functionality such as enabling debugging or presenting special screens or windows that are very useful during development but may leak information or bypass the business logic.</p>
<p>Applications should have logic checks in place to prevent the system from accepting forged requests that may allow attackers the opportunity to exploit the business logic, process, or flow of the application</p>
<p>Example 1: Suppose an e-commerce theater site allows users to select their ticket, apply a onetime 10% Senior discount on the entire sale, view the subtotal and tender the sale. If an attacker is able to see through a proxy that the application has a hidden field (of 1 or 0) used by the business logic to determine if a discount has been taken or not. The attacker is then able to submit the 1 or “no discount has been taken” value multiple times to take advantage of the same discount multiple times.</p>

<h4>Test Integrity Checks</h4>
<p><b>ID: WSTG-BUSL-03</b></p>
<p>Many applications are designed to display different fields depending on the user of situation by leaving some inputs hidden. However, in many cases it is possible to submit values hidden field values to the server using a proxy. In these cases the server-side controls must be smart enough to perform relational or server-side edits to ensure that the proper data is allowed to the server based on user and application specific business logic.</p>
<p>Additionally, the application must not depend on non-editable controls, drop-down menus or hidden fields for business logic processing because these fields remain non-editable only in the context of the browsers. Users may be able to edit their values using proxy editor tools and try to manipulate business logic. If the application exposes values related to business rules like quantity, etc. as non-editable fields it must maintain a copy on the server-side and use the same for business logic processing. <br>Objectives:</p>
<ul>
	<li>Review the project documentation for components of the system that move, store, or handle data.</li>
	<li>Determine what type of data is logically acceptable by the component and what types the system should guard against.</li>
	<li>Determine who should be allowed to modify or read that data in each component.</li>
	<li>Attempt to insert, update, or delete data values used by each component that should not be allowed per the business logic workflow.</li>
</ul>

<h4>Test for Process Timing</h4>
<p><b>ID: WSTG-BUSL-04</b></p>
<p>It is possible that attackers can gather information on an application by monitoring the time it takes to complete a task or give a respond. Additionally, attackers may be able to manipulate and break designed business process flows by simply keeping active sessions open and not submitting their transactions in the “expected” time frame.</p>
<p>Process timing logic vulnerabilities is unique in that these manual misuse cases should be created considering execution and transaction timing that are application/system specific.</p>
<p>Processing timing may give/leak information on what is being done in the application/system background processes. If an application allows users to guess what the particulate next outcome will be by processing time variations, users will be able to adjust accordingly and change behavior based on the expectation and “game the system”.</p>
<p>Example: Many system log on processes ask for the username and password. If you look closely you may be able to see that entering an invalid username and invalid user password takes more time to return an error than entering a valid username and invalid user password. This may allow the attacker to know if they have a valid username and not need to rely on the GUI message.</p>
