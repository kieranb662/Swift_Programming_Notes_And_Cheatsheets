
# HTTP Methods Summary
<table>
  <thead>
    <th>Method</th>
    <th>Meaning</th>
    <th>Syntax</th>
    <th>Request Has Body?</th>
    <th>Successful Response Has Body?</th>
    <th>Safe?</th>
    <th>Indempotent?</th>
    <th>Cacheable?</th>
  </thead>
  <tr>
    <td>GET</td>
    <td>Requests a representation of the specified resource. Requests using GET should only retrieve data.</td>
    <td>GET /index.html</td>
    <td>NO</td>
    <td>YES</td>
    <td>YES</td>
    <td>YES</td>
    <td>YES</td>
  </tr>
  <tr>
    <td>HEAD</td>
    <td>Asks for a response identical to that of a GET request, but without the response body.</td>
    <td>HEAD /index.html</td>
    <td>NO</td>
    <td>YES</td>
    <td>YES</td>
    <td>YES</td>
    <td>YES</td>
  </tr>
  <tr>
    <td>POST</td>
    <td>Used to submit an entity to the specified resource, often causing a change in state or side effects on the server.</td>
    <td>POST /test</td>
    <td>YES</td>
    <td>YES</td>
    <td>NO</td>
    <td>NO</td>
    <td>Only if freshness information is included</td>
  </tr>


  <tr>
    <td>PUT</td>
    <td>Replaces all current representations of the target resource with the request payload.</td>
    <td>PUT /new.html HTTP/1.1 </td>
    <td>YES</td>
    <td>NO</td>
    <td>NO</td>
    <td>YES</td>
    <td>NO</td>
  </tr>
  <tr>
    <td>DELETE</td>
    <td>Deletes the specified resource.</td>
    <td>DELETE /file.html HTTP/1.1 </td>
    <td>MAY</td>
    <td>MAY</td>
    <td>NO</td>
    <td>YES</td>
    <td>NO</td>
  </tr>
  <tr>
    <td>CONNECT</td>
    <td>Establishes a tunnel to the server identified by the target resource.</td>
    <td>CONNECT www.example.com:443 HTTP/1.1</td>
    <td>NO</td>
    <td>YES</td>
    <td>NO</td>
    <td>NO</td>
    <td>NO</td>
  </tr>




  <tr>
    <td>OPTIONS</td>
    <td>Used to describe the communication options for the target resource.</td>
    <td>OPTIONS /index.html HTTP/1.1 <br> OPTIONS * HTTP/1.1</td>
    <td>NO</td>
    <td>YES</td>
    <td>YES</td>
    <td>YES</td>
    <td>NO</td>
  </tr>
  <tr>
    <td>TRACE</td>
    <td>Performs a message loop-back test along the path to the target resource.</td>
    <td>TRACE /index.html</td>
    <td>NO</td>
    <td>NO</td>
    <td>NO</td>
    <td>YES</td>
    <td>NO</td>
  </tr>
  <tr>
    <td>PATCH</td>
    <td>Used to apply partial modifications to a resource.</td>
    <td>PATCH /file.txt HTTP/1.1 </td>
    <td>YES</td>
    <td>YES</td>
    <td>NO</td>
    <td>NO</td>
    <td>NO</td>
  </tr>
</table>

# Status Codes 

<table>
  <thead>
    <tr><th>Code</th>
    <th>Meaning</th>
  </tr></thead>
  <tbody><tr>
    <td>100</td>
    <td><b>Continue</b> - The server has received the request headers and the client should proceed to send the request body</td>
  </tr>
  <tr>
    <td>101</td>
    <td><b>Switching Protocols</b> - The requester has asked the server to switch protocols and the server has agreed to do so.</td>
  </tr>
  <tr>
    <td>102</td>
    <td><b>Processing</b> -  This code indicates that the server has received and is processing the request, but no response is available yet.</td>
  </tr>
  <tr>
    <td>103</td>
    <td><b>Early Hints</b> -  Used to return some response headers before final HTTP message.</td>
  </tr>

  <tr>
    <td>200</td>
    <td><b>OK</b> -  In a GET request, the response will contain an entity corresponding to the requested resource. In a POST request,<br> the response will contain an entity describing or containing the result of the action.</td>
  </tr>
  <tr>
    <td>201</td>
    <td><b>Created</b> - The request has been fulfilled, resulting in the creation of a new resource.</td>
  </tr>
  <tr>
    <td>202</td>
    <td><b>Accepted</b> -  The request has been accepted for processing, but the processing has not been completed. Rquest may be disallowed when processing occurs.</td>
  </tr>
  <tr>
    <td>203</td>
    <td><b>Non-Authoritative Information</b> -  The server is a transforming proxy that received a 200 OK from its origin, but is returning a modified version of the origin's response.</td>
  </tr>


  <tr>
    <td>204</td>
    <td><b>No Content</b> - The server successfully processed the request and is not returning any content.</td>
  </tr>
  <tr>
    <td>205</td>
    <td><b>Reset Content</b> - The server successfully processed the request, but is not returning any content. Unlike a 204 response, this response requires that the requester reset the document view.</td>
  </tr>
  <tr>
    <td>206</td>
    <td><b>Partial Content</b> -  The server is delivering only part of the resource (byte serving) due to a range header sent by the client. <br>Range header used to resume interrupted downloads or split a download into simultaneous streams.</td>
  </tr>
  <tr>
    <td>207</td>
    <td><b>Multi-Status</b> -  The message body that follows is by default an XML message and can contain a number of separate response codes, depending on how many sub-requests were made.</td>
  </tr>
  <tr>
    <td>208</td>
    <td><b>Already Reported</b> -  The members of a DAV binding have already been enumerated in a preceding part of the (multistatus) response, and are not being included again.</td>
  </tr>
  <tr>
    <td>226</td>
    <td><b>IM Used</b> -  The server has fulfilled a request for the resource, and the response is a representation of the result of one or more instance-manipulations applied to the current instance.</td>
  </tr>

  <tr>
    <td>300</td>
    <td><b>Multiple Choices</b> - Indicates multiple options for the resource from which the client may choose.</td>
  </tr>
  <tr>
    <td>301</td>
    <td><b>Moved Permanently</b> - This and all future requests should be directed to the given URI.</td>
  </tr>
  <tr>
    <td>302</td>
    <td><b>Found</b> -  Tells the client to look at (browse to) another URL. 302 has been superseded by 303 and 307.</td>
  </tr>
  <tr>
    <td>303</td>
    <td><b>See Other</b> -  The response to the request can be found under another URI using the GET method. <br>When received in response to a POST (or PUT/DELETE), the client should presume that the server has received the data and should issue a new GET request to the given URI.</td>
  </tr>
  <tr>
    <td>304</td>
    <td><b>Not Modified</b> - Indicates that the resource has not been modified since the version specified by the request headers If-Modified-Since or If-None-Match.</td>
  </tr>
  <tr>
    <td>305</td>
    <td><b>Use Proxy</b> -  The requested resource is available only through a proxy, the address for which is provided in the response.</td>
  </tr>
  <tr>
    <td>306</td>
    <td><b>Switch Proxy</b> -  No longer used. Originally meant "Subsequent requests should use the specified proxy.</td>
  </tr>
  <tr>
    <td>307</td>
    <td><b>Temporary Redirect</b> - In this case, the request should be repeated with another URI; however, future requests should still use the original URI.</td>
  </tr>
  <tr>
    <td>308</td>
    <td><b>Permanent Redirect</b> -  The request and all future requests should be repeated using another URI. 307 and 308 parallel the behaviors of 302 and 301, but do not allow the HTTP method to change.</td>
  </tr>

  <tr>
    <td>400</td>
    <td><b>Bad Request</b> - The server cannot or will not process the request due to an apparent client error.</td>
  </tr>
  <tr>
    <td>401</td>
    <td><b>Unauthorized</b> - Similar to 403 Forbidden, but specifically for use when authentication is required and has failed or has not yet been provided. The response must include a WWW-Authenticate header field containing a challenge applicable to the requested resource.</td>
  </tr>
  <tr>
    <td>402</td>
    <td><b>Payment Required</b> -  Reserved for future use. The original intention was that this code might be used as part of some form of digital cash or micropayment scheme.</td>
  </tr>
  <tr>
    <td>403</td>
    <td><b>Forbidden</b> -  The request was valid, but the server is refusing action.</td>
  </tr>
  <tr>
    <td>404</td>
    <td><b>Not Found</b> - The requested resource could not be found but may be available in the future. Subsequent requests by the client are permissible.</td>
  </tr>
  <tr>
    <td>405</td>
    <td><b>Method Not Allowed</b> -  A request method is not supported for the requested resource; for example, a GET request on a form that requires data to be presented via POST, or a PUT request on a read-only resource.</td>
  </tr>
  <tr>
    <td>406</td>
    <td><b>Not Acceptable</b> -  The requested resource is capable of generating only content not acceptable according to the Accept headers sent in the request.</td>
  </tr>
  <tr>
    <td>407</td>
    <td><b>Proxy Authentication Required</b> - The client must first authenticate itself with the proxy.</td>
  </tr>
  <tr>
    <td><b>408</b></td>
    <td><b>Request Timeout</b> - The server timed out waiting for the request.  The client MAY repeat the request without modifications at any later time.</td>
  </tr>





  <tr>
    <td>409</td>
    <td><b>Conflict</b> - Indicates that the request could not be processed because of conflict in the current state of the resource, such as an edit conflict between multiple simultaneous updates.</td>
  </tr>
  <tr>
    <td>410</td>
    <td><b>Gone</b> - Indicates that the resource requested is no longer available and will not be available again.</td>
  </tr>
  <tr>
    <td>411</td>
    <td><b>Length Required</b> -  The request did not specify the length of its content, which is required by the requested resource.</td>
  </tr>
  <tr>
    <td>412</td>
    <td><b>Precondition Failed</b> -  The server does not meet one of the preconditions that the requester put on the request header fields.</td>
  </tr>
  <tr>
    <td>413</td>
    <td><b>Payload Too Large</b> - The request is larger than the server is willing or able to process.</td>
  </tr>
  <tr>
    <td>414</td>
    <td><b>URI Too Long</b> -  The URI provided was too long for the server to process. Often the result of too much data being encoded as a query-string of a GET request, in which case it should be converted to a POST request</td>
  </tr>
  <tr>
    <td>415</td>
    <td><b>Unsupported Media Type</b> -  The request entity has a media type which the server or resource does not support.</td>
  </tr>
  <tr>
    <td>416</td>
    <td> <b>Range Not Satisfiable</b> - The client has asked for a portion of the file (byte serving), but the server cannot supply that portion.</td>
  </tr>
  <tr>
    <td>417</td>
    <td><b>Expectation Failed</b> - The server cannot meet the requirements of the Expect request-header field.</td>
  </tr>




  <tr>
    <td>421</td>
    <td><b>Misdirected Request</b> - The request was directed at a server that is not able to produce a response.</td>
  </tr>
  <tr>
    <td>422</td>
    <td> <b>Unprocessable Entity</b> - The request was well-formed but was unable to be followed due to semantic errors.</td>
  </tr>
  <tr>
    <td>423</td>
    <td> <b>Locked</b> -  The resource that is being accessed is locked.</td>
  </tr>
  <tr>
    <td>424</td>
    <td><b>Failed Dependency</b> -  The request failed because it depended on another request and that request failed .</td>
  </tr>
  <tr>
    <td>425</td>
    <td><b>Too Early</b> - Indicates that the server is unwilling to risk processing a request that might be replayed.</td>
  </tr>
  <tr>
    <td>426</td>
    <td><b>Upgrade Required</b> -  The client should switch to a different protocol such as TLS/1.0, given in the Upgrade header field.</td>
  </tr>
  <tr>
    <td>428</td>
    <td><b>Precondition Required</b> -  The origin server requires the request to be conditional.</td>
  </tr>
  <tr>
    <td>429</td>
    <td> <b>Too Many Requests</b> - The user has sent too many requests in a given amount of time. Intended for use with rate-limiting schemes.</td>
  </tr>
  <tr>
    <td>431</td>
    <td><b>Request Header Fields Too Large</b>  - The server is unwilling to process the request because either an individual header field, or all the header fields collectively, are too large.</td>
  </tr>
  <tr>
    <td>451</td>
    <td><b>Unavailable For Legal Reasons</b>  - A server operator has received a legal demand to deny access to a resource or to a set of resources that includes the requested resource.</td>
  </tr>






  <tr>
    <td>500</td>
    <td><b>Internal Server Error</b> - A generic error message, given when an unexpected condition was encountered and no more specific message is suitable.</td>
  </tr>
  <tr>
    <td>501</td>
    <td> <b>Not Implemented</b> - The server either does not recognize the request method, or it lacks the ability to fulfil the request. Usually this implies future availability.</td>
  </tr>
  <tr>
    <td>502</td>
    <td> <b>Bad Gateway</b> -  The server was acting as a gateway or proxy and received an invalid response from the upstream server.</td>
  </tr>
  <tr>
    <td>503</td>
    <td> <b>Service Unavailable</b> -  The server cannot handle the request (because it is overloaded or down for maintenance). Generally, this is a temporary state.</td>
  </tr>
  <tr>
    <td>504</td>
    <td><b>Gateway Timeout</b> - The server was acting as a gateway or proxy and did not receive a timely response from the upstream server.</td>
  </tr>
  <tr>
    <td>505</td>
    <td><b>HTTP Version Not Supported</b> - The server does not support the HTTP protocol version used in the request.</td>
  </tr>
  <tr>
    <td>506</td>
    <td> <b>Variant Also Negotiates</b> -  Transparent content negotiation for the request results in a circular reference.</td>
  </tr>
  <tr>
    <td>507</td>
    <td> <b>Insufficient Storage</b>  - The server is unable to store the representation needed to complete the request.</td>
  </tr>
  <tr>
    <td>508</td>
    <td> <b>Loop Detected</b>  - The server detected an infinite loop while processing the request (sent instead of 208 Already Reported).</td>
  </tr>
  <tr>
    <td>510</td>
    <td><b>Not Extended</b>  - Further extensions to the request are required for the server to fulfil it.</td>
  </tr>
  <tr>
    <td>511</td>
    <td><b>Network Authentication Required</b> - The client needs to authenticate to gain network access. Intended for use by intercepting proxies used to control access to the network.</td>
  </tr>
</tbody></table>

# MIME Types 

<table class="standard-table">
 <thead>
  <tr>
   <th scope="col">Extension</th>
   <th scope="col">Kind of document</th>
   <th scope="col">MIME Type</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code>.aac</code></td>
   <td>AAC audio</td>
   <td><code>audio/aac</code></td>
  </tr>
  <tr>
   <td><code>.abw</code></td>
   <td>AbiWord document</td>
   <td><code>application/x-abiword</code></td>
  </tr>
  <tr>
   <td><code>.arc</code></td>
   <td>Archive document (multiple files embedded)</td>
   <td><code>application/x-freearc</code></td>
  </tr>
  <tr>
   <td><code>.avi</code></td>
   <td>AVI: Audio Video Interleave</td>
   <td><code>video/x-msvideo</code></td>
  </tr>
  <tr>
   <td><code>.azw</code></td>
   <td>Amazon Kindle eBook format</td>
   <td><code>application/vnd.amazon.ebook</code></td>
  </tr>
  <tr>
   <td><code>.bin</code></td>
   <td>Any kind of binary data</td>
   <td><code>application/octet-stream</code></td>
  </tr>
  <tr>
   <td><code>.bmp</code></td>
   <td>Windows OS/2 Bitmap Graphics</td>
   <td><code>image/bmp</code></td>
  </tr>
  <tr>
   <td><code>.bz</code></td>
   <td>BZip archive</td>
   <td><code>application/x-bzip</code></td>
  </tr>
  <tr>
   <td><code>.bz2</code></td>
   <td>BZip2 archive</td>
   <td><code>application/x-bzip2</code></td>
  </tr>
  <tr>
   <td><code>.csh</code></td>
   <td>C-Shell script</td>
   <td><code>application/x-csh</code></td>
  </tr>
  <tr>
   <td><code>.css</code></td>
   <td>Cascading Style Sheets (CSS)</td>
   <td><code>text/css</code></td>
  </tr>
  <tr>
   <td><code>.csv</code></td>
   <td>Comma-separated values (CSV)</td>
   <td><code>text/csv</code></td>
  </tr>
  <tr>
   <td><code>.doc</code></td>
   <td>Microsoft Word</td>
   <td><code>application/msword</code></td>
  </tr>
  <tr>
   <td><code>.docx</code></td>
   <td>Microsoft Word (OpenXML)</td>
   <td><code>application/vnd.openxmlformats-officedocument.wordprocessingml.document</code></td>
  </tr>
  <tr>
   <td><code>.eot</code></td>
   <td>MS Embedded OpenType fonts</td>
   <td><code>application/vnd.ms-fontobject</code></td>
  </tr>
  <tr>
   <td><code>.epub</code></td>
   <td>Electronic publication (EPUB)</td>
   <td><code>application/epub+zip</code></td>
  </tr>
  <tr>
   <td><code>.gif</code></td>
   <td>Graphics Interchange Format (GIF)</td>
   <td><code>image/gif</code></td>
  </tr>
  <tr>
   <td><code>.htm<br>
    .html</code></td>
   <td>HyperText Markup Language (HTML)</td>
   <td><code>text/html</code></td>
  </tr>
  <tr>
   <td><code>.ico</code></td>
   <td>Icon format</td>
   <td><code>image/vnd.microsoft.icon</code></td>
  </tr>
  <tr>
   <td><code>.ics</code></td>
   <td>iCalendar format</td>
   <td><code>text/calendar</code></td>
  </tr>
  <tr>
   <td><code>.jar</code></td>
   <td>Java Archive (JAR)</td>
   <td><code>application/java-archive</code></td>
  </tr>
  <tr>
   <td><code>.jpeg</code><br>
    <code>.jpg</code></td>
   <td>JPEG images</td>
   <td><code>image/jpeg</code></td>
  </tr>
  <tr>
   <td><code>.js</code></td>
   <td>JavaScript</td>
   <td><code>text/javascript</code></td>
  </tr>
  <tr>
   <td><code>.json</code></td>
   <td>JSON format</td>
   <td><code>application/json</code></td>
  </tr>
  <tr>
   <td><code>.jsonld</code></td>
   <td>JSON-LD format</td>
   <td><code>application/ld+json</code></td>
  </tr>
  <tr>
   <td><code>.mid</code><br>
    <code>.midi</code></td>
   <td>Musical Instrument Digital Interface (MIDI)</td>
   <td><code>audio/midi</code> <code>audio/x-midi</code></td>
  </tr>
  <tr>
   <td><code>.mjs</code></td>
   <td>JavaScript module</td>
   <td><code>text/javascript</code></td>
  </tr>
  <tr>
   <td><code>.mp3</code></td>
   <td>MP3 audio</td>
   <td><code>audio/mpeg</code></td>
  </tr>
  <tr>
   <td><code>.mpeg</code></td>
   <td>MPEG Video</td>
   <td><code>video/mpeg</code></td>
  </tr>
  <tr>
   <td><code>.mpkg</code></td>
   <td>Apple Installer Package</td>
   <td><code>application/vnd.apple.installer+xml</code></td>
  </tr>
  <tr>
   <td><code>.odp</code></td>
   <td>OpenDocument presentation document</td>
   <td><code>application/vnd.oasis.opendocument.presentation</code></td>
  </tr>
  <tr>
   <td><code>.ods</code></td>
   <td>OpenDocument spreadsheet document</td>
   <td><code>application/vnd.oasis.opendocument.spreadsheet</code></td>
  </tr>
  <tr>
   <td><code>.odt</code></td>
   <td>OpenDocument text document</td>
   <td><code>application/vnd.oasis.opendocument.text</code></td>
  </tr>
  <tr>
   <td><code>.oga</code></td>
   <td>OGG audio</td>
   <td><code>audio/ogg</code></td>
  </tr>
  <tr>
   <td><code>.ogv</code></td>
   <td>OGG video</td>
   <td><code>video/ogg</code></td>
  </tr>
  <tr>
   <td><code>.ogx</code></td>
   <td>OGG</td>
   <td><code>application/ogg</code></td>
  </tr>
  <tr>
   <td><code>.otf</code></td>
   <td>OpenType font</td>
   <td><code>font/otf</code></td>
  </tr>
  <tr>
   <td><code>.png</code></td>
   <td>Portable Network Graphics</td>
   <td><code>image/png</code></td>
  </tr>
  <tr>
   <td><code>.pdf</code></td>
   <td>Adobe Portable Document Format(PDF)</td>
   <td><code>application/pdf</code></td>
  </tr>
  <tr>
   <td><code>.ppt</code></td>
   <td>Microsoft PowerPoint</td>
   <td><code>application/vnd.ms-powerpoint</code></td>
  </tr>
  <tr>
   <td><code>.pptx</code></td>
   <td>Microsoft PowerPoint (OpenXML)</td>
   <td><code>application/vnd.openxmlformats-officedocument.presentationml.presentation</code></td>
  </tr>
  <tr>
   <td><code>.rar</code></td>
   <td>RAR archive</td>
   <td><code>application/x-rar-compressed</code></td>
  </tr>
  <tr>
   <td><code>.rtf</code></td>
   <td>Rich Text Format (RTF)</td>
   <td><code>application/rtf</code></td>
  </tr>
  <tr>
   <td><code>.sh</code></td>
   <td>Bourne shell script</td>
   <td><code>application/x-sh</code></td>
  </tr>
  <tr>
   <td><code>.svg</code></td>
   <td>Scalable Vector Graphics (SVG)</td>
   <td><code>image/svg+xml</code></td>
  </tr>
  <tr>
   <td><code>.swf</code></td>
   <td>Small web format(SWF) or Adobe Flash document</td>
   <td><code>application/x-shockwave-flash</code></td>
  </tr>
  <tr>
   <td><code>.tar</code></td>
   <td>Tape Archive (TAR)</td>
   <td><code>application/x-tar</code></td>
  </tr>
  <tr>
   <td><code>.tif<br>
    .tiff</code></td>
   <td>Tagged Image File Format (TIFF)</td>
   <td><code>image/tiff</code></td>
  </tr>
  <tr>
   <td><code>.ts</code></td>
   <td>MPEG transport stream</td>
   <td><code>video/mp2t</code></td>
  </tr>
  <tr>
   <td><code>.ttf</code></td>
   <td>TrueType Font</td>
   <td><code>font/ttf</code></td>
  </tr>
  <tr>
   <td><code>.txt</code></td>
   <td>Text, (generally ASCII or ISO 8859-<em>n</em>)</td>
   <td><code>text/plain</code></td>
  </tr>
  <tr>
   <td><code>.vsd</code></td>
   <td>Microsoft Visio</td>
   <td><code>application/vnd.visio</code></td>
  </tr>
  <tr>
   <td><code>.wav</code></td>
   <td>Waveform Audio Format</td>
   <td><code>audio/wav</code></td>
  </tr>
  <tr>
   <td><code>.weba</code></td>
   <td>WEBM audio</td>
   <td><code>audio/webm</code></td>
  </tr>
  <tr>
   <td><code>.webm</code></td>
   <td>WEBM video</td>
   <td><code>video/webm</code></td>
  </tr>
  <tr>
   <td><code>.webp</code></td>
   <td>WEBP image</td>
   <td><code>image/webp</code></td>
  </tr>
  <tr>
   <td><code>.woff</code></td>
   <td>Web Open Font Format (WOFF)</td>
   <td><code>font/woff</code></td>
  </tr>
  <tr>
   <td><code>.woff2</code></td>
   <td>Web Open Font Format (WOFF)</td>
   <td><code>font/woff2</code></td>
  </tr>
  <tr>
   <td><code>.xhtml</code></td>
   <td>XHTML</td>
   <td><code>application/xhtml+xml</code></td>
  </tr>
  <tr>
   <td><code>.xls</code></td>
   <td>Microsoft Excel</td>
   <td><code>application/vnd.ms-excel</code></td>
  </tr>
  <tr>
   <td><code>.xlsx</code></td>
   <td>Microsoft Excel (OpenXML)</td>
   <td><code>application/vnd.openxmlformats-officedocument.spreadsheetml.sheet</code></td>
  </tr>
  <tr>
   <td><code>.xml</code></td>
   <td><code>XML</code></td>
   <td><code>application/xml </code><br><code>text/xml</code></td>
  </tr>
  <tr>
   <td><code>.xul</code></td>
   <td>XUL</td>
   <td><code>application/vnd.mozilla.xul+xml</code></td>
  </tr>
  <tr>
   <td><code>.zip</code></td>
   <td>ZIP archive</td>
   <td><code>application/zip</code></td>
  </tr>
  <tr>
   <td><code>.3gp</code></td>
   <td> audio/video container</td>
   <td><code>video/3gpp</code><br>
    <code>audio/3gpp</code> if it doesn't contain video</td>
  </tr>
  <tr>
   <td><code>.3g2</code></td>
   <td> audio/video container</td>
   <td><code>video/3gpp2</code><br>
    <code>audio/3gpp2</code> if it doesn't contain video</td>
  </tr>
  <tr>
   <td><code>.7z</code></td>
   <td> archive </td>
   <td><code>application/x-7z-compressed</code></td>
  </tr>
 </tbody>
</table>

<h1>Cross-Origin Reference Sharing</h1>
<p>Requests come in two categories</p>
<ul>
  <li>Simple Requests </li>
  <li>Preflight Requests</li>
</ul>
<table>
  <thead>
    <th colspan="2" style="text-align: center"> Simple</th>
  </thead>
  <tr>
    <th>Allowed Methods</th>
    <td>GET <br> HEAD <br> POST</td>
  </tr>
  <tr>
    <th>Allowed Headers</th>
    <td>Accept <br> Accept-Language <br> Connection<br> Content-Type <br> DPR <br> Downlink <br> Save-Data <br> User-Agent<br> Viewport-Width <br> Width </td>
  </tr>
  <tr>
    <th>Allowed Content-Type</th>
    <td>application/x-www-form-urlencoded <br> multipart/form-data <br> text/plain</td>
  </tr>
</table>

<table>
  <thead>
    <th colspan="2" style="text-align: center"> Preflight</th>
  </thead>
  <tr>
    <th>Trigger Methods</th>
    <td>PUT <br> DELETE <br> CONNECT <br> OPTIONS <br> TRACE <br> PATCH</td>
  </tr>
  <tr>
    <th>Triggered By Anything <br> But These Headers</th>
    <td>Accept <br> Accept-Language <br> Connection<br> Content-Type <br> DPR <br> Downlink <br> Save-Data <br> User-Agent<br> Viewport-Width <br> Width </td>
  </tr>
  <tr>
    <th>Triggered By Anything But <br> These Content-Types</th>
    <td>application/x-www-form-urlencoded <br> multipart/form-data <br> text/plain</td>
  </tr>
</table>

<table>
  <thead>
    <th colspan="2" style="text-align: center"> CORS Request Headers</th>
  </thead>
  <tr>
    <td>Origin:</td>
    <td>Value can be null, or a URI</td>
  </tr>
  <tr>
    <td>Access-Control-Request-Method:</td>
    <td>Value is the method to be <br> used during the actual request.</td>
  </tr>
  <tr>
    <td>Access-Control-Request-Headers:</td>
    <td>Value is either a single header <br> or a list of comma separated headers. </td>
  </tr>
</table>



<table>
  <thead>
    <th colspan="2" style="text-align: center"> CORS Response Headers</th>
  </thead>
  <tr>
    <td>Access-Control-Allow-Origin:</td>
    <td>specifies either a single origin, <br> which tells browsers to allow that <br> origin to access the resource; or else <br> — for requests without credentials — <br> the "*" wildcard, to tell browsers to allow <br> any origin to access the resource.</td>
  </tr>
  <tr>
    <td>Access-Control-Expose-Headers:</td>
    <td>header lets a server whitelist headers <br> that browsers are allowed to access.</td>
  </tr>
  <tr>
    <td>Access-Control-Max-Age:</td>
    <td> indicates how long the results of a <br> preflight request can be cached. <br> (seconds) </td>
  </tr>
  <tr>
    <td>Access-Control-Allow-Credentials:</td>
    <td> Indicates whether or not the response to the request can be exposed when the credentials flag is true. </td>
  </tr>
  <tr>
    <td>Access-Control-Allow-Methods:</td>
    <td> specifies the method or methods allowed when accessing the resource. </td>
  </tr>
  <tr>
    <td>Access-Control-Allow-Headers:</td>
    <td> used in response to a preflight request to indicate which HTTP headers can be used when making the actual request. </td>
  </tr>
</table>

<h2>Important Concepts</h2>
  <h3>Same-Origin Policy(SOP)</h3>
  <p> Put simply a web browser permits scripts contained in the first webpage to access data in the second only if both have the same origin.</p>
  <p><b>Origin</b> - A combination of URI scheme, host name, and port number.</p>
  <p>This policy is highly dependent on HTTP Cookies to maintain authenticated user sessions. A strict separation between content provided by
      unrelated sites must be maintained on the client side</p>
  <p>This policy only refers to scripts. Images, CSS and dynamically-loaded scripts all can be accessed across origins using the corresponding HTML tags. </p>

  <h3>Cross-Site Scripting(XSS) </h3>
  <p>An attack that exploits the trust a user has for a particular site. Enables attackers to inject client side scripts into webpages viewed by other users. These attacks take advantage of a wide variety of flaws, but can be classified into two groups.</p>
  <ul>
    <li><b>Non-persistant(reflected)</b>
      <ul>
        <li>When data provided by a web client(such as an HTML form), is used immediatly by server side scripts to parse and display a page of results for the user, without proper sanitation. The data provided by the user could easily have injected code that is now in the resulting page.</li>
        <li>Most commonly delivered via email or a neutral web site.</li>
      </ul>
    </li>
    <li><b>Persistant(stored)</b>
      <ul>
        <li>Occurs when data provided by the attacker is saved by the server and then permanently displayed on normal pages.</li>
        <li>Common on message boards that allow users to submit HTML formatted messages for others to read.</li>
      </ul>
    </li>
  </ul>
  <h4>Prevention</h4>
  <p>Methods include Contextual output encoding/escaping of string input, Safely validating untrusted HTML input, cookie security, and disabling scripts.</p>
  <p>Using <b>Content-Security-Policy(CSP)</b>  to selectively disable scripts helps reduce the rate of successful attacks. Only allowing trusted scripts and disallowing dynamic code loading.</p>


  <h3>Cross-Site Request Forgery(CSRF)</h3>
<p>A malicious exploit of a website where unauthorized commands are transmitted from a user that the web application trusts.
    Not even GET or POST is safe. These can be exploited and must be used properly to avoid manipulation.
    With regards to POST you must keep an eye out for malicious HTML forms.</p>
    <p> These attacks take advantage of the fact that the same origin policy does not apply to HTML tags.</p>
<h4>Common characteristics</h4>
<ul>
  <li>Involves sites that rely on a user's identity</li>
  <li>Exploits the site's trust in that identity</li>
  <li>Tricks browser into sending HTTP requests to a target site</li>
  <li>Involves HTTP requests that have side effects (ex. DELETE, PUT)</li>
</ul>
<h4>Prevention</h4>
<p>General prevention procedures make use of embedded authentication data within requests so that unauthorized locations can be detected.</p>

<ul>
  <li><b>Synchronizer Token Pattern(STP)</b>
  <ul>
    <li>Token, secret, and unique value for each request, is embedded by the web application in all HTML forms.</li>
    <li>These forms are then verified server side.</li>
    <li>Most compatible method as it relies only on HTML.</li>
    <li>Large cost serverside to validate tokens as they are unique and unpredictable.</li>
  </ul>
</li>
<li><b>Cookie-to-header token</b>
  <ul>
    <li>Mainly Javascript applications use this technique</li>
    <li>Relies on the same-origin policy. A site may not disable this policy or it will be vulnerable</li>
    <li> On initial visit without an associated server session, The app sets a cookie containing a random token that remains for the entirety of the session.</li>
    <li>Client side Javascript, reads and copies the value into a custom HTTP header to be sent with each transactional request.</li>
    <li>Then the server validates the token.</li>
  </ul>
</li>
<li><b>Double Submit Cookie</b>
    <ul>
      <li> Similar to cookie-to-header only this does not involve javascript.</li>
      <li>A site sets a CSRF token as a cookie and inserts it as a hidden field in each HTML form sent to the client.</li>
      <li>SOP prevents an attacker from reading or setting cookies on the target domain.</li>
      <li>Tokens do not need to be stored on the server.</li>
    </ul></li>
</ul>

