Nam Km
VULNERABILITY FOUND
1. Missing "Stric-Transport-Security" header 
	The HTTP protocol by itself is clear text, meaning that any data that is transmitted via HTTP can be captured and the contents viewed. To keep data private and prevent it from being intercepted, HTTP is often tunnelled through either Secure Sockets Layer (SSL) or Transport Layer Security (TLS). When either of these encryption standards are used, it is referred to as HTTPS.HTTP Strict Transport Security (HSTS) is an optional response header that can be configured on the server to instruct the browser to only communicate via HTTPS. This will be enforced by the browser even if the user requests a HTTP resource on the same server.Cyber-criminals will often attempt to compromise sensitive information passed from the client to the server using HTTP. This can be conducted via various Man-in-The-Middle (MiTM) attacks or through network packet captures.
	Arachni discovered that the affected application is using HTTPS however does not use the HSTS header.
2. Missing "X-Frame-Options" header
	Clickjacking (User Interface redress attack, UI redress attack, UI redressing) is a malicious technique of tricking a Web user into clicking on something different from what the user perceives they are clicking on, thus potentially revealing confidential information or taking control of their computer while clicking on seemingly innocuous web pages.The server didnΓÇÖt return an X-Frame-Options header which means that this website could be at risk of a clickjacking attack.The X-Frame-Options HTTP response header can be used to indicate whether or not a browser should be allowed to render a page inside a frame or iframe. Sites can use this to avoid clickjacking attacks, by ensuring that their content is not embedded into other sites.
3. Interesting response
	The server responded with a non 200 (OK) nor 404 (Not Found) status code. This is a non-issue, however exotic HTTP response status codes can provide useful insights into the behavior of the web application and assist with the penetration test.
4. Insecure cookie
	HTTP by itself is a stateless protocol. Therefore the server is unable to determine which requests are performed by which client, and which clients are authenticated or unauthenticated.The use of HTTP cookies within the headers, allows a web server to identify each individual client and can therefore determine which clients hold valid authentication, from those that do not. These are known as session cookies.When a cookie is set by the server (sent the header of an HTTP response) there are several flags that can be set to configure the properties of the cookie and how it is to be handled by the browser.One of these flags is known as the secure flag. When the secure flag is set, the browser will prevent it from being sent over a clear text channel (HTTP) and only allow it to be sent when an encrypted channel is used (HTTPS).Arachni discovered that a cookie was set by the server without the secure flag being set. Although the initial setting of this cookie was via an HTTPS connection, any HTTP link to the same server will result in the cookie being send in clear text.

