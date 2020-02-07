# APIs 

<h2> Different Files to be received </h2>

1. JSON
2. XML
3. Images
4. Video

<h2> Types of APIs </h2>

1. **SOAP**(Simple Object Access Protocol):
Uses proprietary XML format to transfer data. main function is to define structure
of messages and method of communication. Also uses WSDL(Web Services Definition Language),
in a machine readable document to publish a definition of its interface

**Example Request**
```XML
POST /InStock HTTP/1.1
Host: www.example.org
Content-Type: application/soap+xml; charset=utf-8
Content-Length: nnn

<?xml version="1.0"?>

<soap:Envelope
xmlns:soap="http://www.w3.org/2003/05/soap-envelope/"
soap:encodingStyle="http://www.w3.org/2003/05/soap-encoding">

<soap:Body xmlns:m="http://www.example.org/stock">
  <m:GetStockPrice>
    <m:StockName>IBM</m:StockName>
  </m:GetStockPrice>
</soap:Body>

</soap:Envelope>
```

**Example Response**
```XML
HTTP/1.1 200 OK
Content-Type: application/soap+xml; charset=utf-8
Content-Length: nnn

<?xml version="1.0"?>

<soap:Envelope
xmlns:soap="http://www.w3.org/2003/05/soap-envelope/"
soap:encodingStyle="http://www.w3.org/2003/05/soap-encoding">

<soap:Body xmlns:m="http://www.example.org/stock">
  <m:GetStockPriceResponse>
    <m:Price>34.5</m:Price>
  </m:GetStockPriceResponse>
</soap:Body>

</soap:Envelope>
```

2. **XML-RPC**: uses a specific XML to transfer data

3. **JSON-RPC**: similar to XML only uses JSON

4. **REST**(Representational State Transfer): Not a protocol but a set of architectural principles.

**Example XML Sign in Request**
```XML
POST /api/2.2/auth/signin HTTP/1.1
HOST: my-server
Content-Type:text/xml

<tsRequest>
  <credentials name="administrator" password="passw0rd">
    <site contentUrl="" />
  </credentials>
</tsRequest>
```
**Example JSON Sign in Request**
```JSON
POST /api/2.2/auth/signin HTTP/1.1
HOST: my-server
Content-Type:application/json
Accept:application/json

{
  "credentials": {
    "name": "administrator",
    "password": "passw0rd",
    "site": {
      "contentUrl": ""
    }
  }
}

```

**Example GET List of Resources**
```
GET /api/2.2/sites/9a8b7c6d-5e4f-3a2b-1c0d-9e8f7a6b5c4d/users/users HTTP/1.1
HOST: my-server
X-Tableau-Auth: 12ab34cd56ef78ab90cd12ef34ab56cd
```
**Example XML Create New Resources**
```XML
POST /api/2.2/sites/9a8b7c6d-5e4f-3a2b-1c0d-9e8f7a6b5c4d/users HTTP/1.1
HOST: my-server
X-Tableau-Auth: 12ab34cd56ef78ab90cd12ef34ab56cd
Content-Type: text/xml

<tsRequest>
  <user name="NewUser" siteRole="Publisher" />
</tsRequest>
```

**Example JSON Create New Resources**
```JSON
POST /api/2.2/sites/9a8b7c6d-5e4f-3a2b-1c0d-9e8f7a6b5c4d/users HTTP/1.1
HOST: my-server
X-Tableau-Auth: 12ab34cd56ef78ab90cd12ef34ab56cd
Content-Type: application/json

{
  "user": {
    "name": "NewUser1",
    "siteRole":  "Publisher"
  }
}

```
**Example XML Update a Resource**
```XML
PUT /api/2.2/sites/9a8b7c6d-5e4f-3a2b-1c0d-9e8f7a6b5c4d/users/9f9e9d9c-8b8a-8f8e-7d7c-7b7a6f6d6e6d HTTP/1.1
HOST: my-server
X-Tableau-Auth: 12ab34cd56ef78ab90cd12ef34ab56cd
Content-Type: text/xml

<tsRequest>
  <user fullName="NewUser2" siteRole="ViewerWithPublish" />
</tsRequest>
```
**Example JSON Update a Resource**
```JSON
PUT /api/2.2/sites/9a8b7c6d-5e4f-3a2b-1c0d-9e8f7a6b5c4d/users/9f9e9d9c-8b8a-8f8e-7d7c-7b7a6f6d6e6d HTTP/1.1
HOST: my-server
X-Tableau-Auth: 12ab34cd56ef78ab90cd12ef34ab56cd
Content-Type: application/json

{
  "user": {
    "fullName": "NewUser2",
    "siteRole":  "ViewerWithPublish"
  }
}

```
**Example Delete a Resource**
```
DELETE /api/2.2/sites/d0356794-bb9d-4c5c-b43d-ec384a2baf5a/users/2798bf2f-964d-4cf6-994a-0744c4555f84 HTTP/1.1
HOST: my-server
X-Tableau-Auth: 12ab34cd56ef78ab90cd12ef34ab56cd
```

## Comparison Summary

<table>
        <tr>
            <th>SOAP</th>
            <th>REST</th>
        </tr>
        <tr>
          <td> Strict set of rules and advanced security to follow </td>
          <td> Loose guidelines to follow and allow developers to make recommendations easily.</td>
        </tr>
        <tr>
          <td> Sends messages in <b>XML</b> format.
          </td>
          <td>  Can send plain text, <b>HTML</b>, <b>XML</b>, <b>YAML</b>, and <b>JSON</b>. </td>
        </tr>
        <tr>
          <td> Requires an Envelope and Body. Headers and Faults are optional
          </td>
          <td> Client-Server separation - each act independently and interact only thru requests and responses</td>
        </tr>
        <tr>
          <td>
          </td>
          <td>  Uniform interface- requests from different clients should look the same. Same resources shouldn't have more than on URI </td>
        </tr>
        <tr>
          <td> API calls cannot be cached
          </td>
          <td>  Cacheable Resources </td>
        </tr>
        <tr>
          <td>
          </td>
          <td>  Layered System </td>
        </tr>
        <tr>
          <td> Driven by function  </td>
          <td> Driven by data</td>
        </tr>
        <tr>
          <td> requires more bandwidth </td>
          <td> requires minimal bandwidth</td>
        </tr>
        <tr>
          <td>
          default Stateless but can be made stateful.
          sends messages using other protocols such as <b>HTTP</b> , <b>SMTP</b>(Simple Mail Transfer Protocol) <b>TCP</b>, or <b>UDP</b></td>
          <td> Stateless existence and use of <b>HTTP</b> status codes</td>
        </tr>

# URLSession Template

```Swift 
class <# Name #>: NSObject {
    
    /// Handles the setup, requesting and handling of responses.
    func requestData() {
        
        // Insert initial URL String here.
        let urlString = <# String #>
        let url = URL(string: urlString)
        
        /// Create the request
        var request = URLRequest(url: url!)
        
        /// REQUIRED
        request.httpMethod = <# Method #>
        
        // Usually the created from a string that uses `String.Encoding.utf8`.
        // If adding a body make sure to include the HeaderField "Content-Length" with the length of the message as the value,
        // and the corresponding "Content-Type"
        request.httpBody = <# Data #>
        
        // Add values as needed.
        request.addValue(<# Value #>, forHTTPHeaderField: <# Field #>)
        
        
        /// The session data task that requests and handles initial data, response, and error procedures.
        let task = URLSession(configuration: .default).dataTask(with: request) { data, response, error in
            
            // Create views or actions here for handling errors
            
            
            if let error = error {
                // call a method for handling client errors.
                // If updating the UI then remember to call `DispatchQueue.main.async
                return
            }
            
            
            // Check the respones for important Error Codes here
            guard let httpResponse = response as? HTTPURLResponse else {
                    // Call a method for handling the server error
                    return
            }
            
            
            // It is also a good idea to check if the MIME Type is the expected type.
            if let mimeType = httpResponse.mimeType, mimeType == <# MIME Type #>, data = data {
               
                // Do something with the data.
                
                
                // IMPORTANT - the completion handler is called on a Different Grand Central Dispatch Queue than the task creator.
                // Call methods for updating the UI here.
                DispatchQueue.main.async {
                    <#code#>
                }
            }
        }
        // Tasks are created in the suspended state.
        task.resume()
    }
}
```

## Background Download

```Swift
/// - Important
///
///1. If your app is in the background, the system may suspend your app while the download is performed in another process.
///   In this case, when the download finishes, the system resumes the app and calls
///   application(_:handleEventsForBackgroundURLSession:completionHandler:)
///
///
///2. Store the completionHandler in an accessible location
///
///
///3. Use this format to handle the URLSessionDelegate call
///
///
///   ```
///        func urlSessionDidFinishEvents(forBackgroundURLSession session: URLSession) {
///           // May be called on a secondary queue, return back to main queue
///            DispatchQueue.main.async {
///               // In this case the completionHandler was stored within the UIApplication
///                guard let appDelegate = UIApplication.shared.delegate as? AppDelegate,
///                    let backgroundCompletionHandler =
///                    appDelegate.backgroundCompletionHandler else {
///                       return
///                }
///                backgroundCompletionHandler()
///           }
///        } ```
///
///4. urlSession(_:downloadTask:didFinishDownloadingTo:) is called,
///   file is available until this method returns. Perform reading and saving here
///
///
///
/// - Note
///   * Session must provide a delegate for event delivery.
///   * Only HTTP and HTTPS protocols are supported.
///   * Redirects are always followed,
///       urlSession(_:task:willPerformHTTPRedirection:newRequest:completionHandler:)
///       will **NOT** be called.
///   * If app is terminated while suspended, recreate background session within launch time setup.
///
///
class <# Name #>: NSObject {
    
    /// Background download session
    private lazy var <# Session Name #>: URLSession = {
        // Create a unique configuration identifier.
        let config = URLSessionConfiguration.background(withIdentifier: <# identifier #>)
        // true means that app waits for optimal conditions before performing transfer
        // use false for time-sensitive tasks.
        config.isDiscretionary = true
        // allows the system to wake up app when task completes and app is in the background.
        config.sessionSendsLaunchEvents = true
        return URLSession(configuration: config, delegate: <# URLSessionDelegate #>, delegateQueue: nil)
    }()
    

    /// Creates and starts the background download task
    func setUpTask() {
        
        // Insert initial URL String here.
        let urlString = <# String #>
        let url = URL(string: urlString)
        
        /// Create the request
        var request = URLRequest(url: url!)
        
        /// REQUIRED
        request.httpMethod = <# Method #>
        
        // Usually the created from a string that uses `String.Encoding.utf8`.
        // If adding a body make sure to include the HeaderField "Content-Length" with the length of the message as the value,
        // and the corresponding "Content-Type"
        request.httpBody = <# Data #>
        
        // Add values as needed.
        request.addValue(<# Value #>, forHTTPHeaderField: <# Field #>)
        
        let backgroundTask = <# Session Name #>.downloadTask(with: <# URL or URLRequest #>)
        backgroundTask.earliestBeginDate = Date().addingTimeInterval(<# Interval(seconds) #>)
        backgroundTask.countOfBytesClientExpectsToSend =  <# Sent Bytes #>
        backgroundTask.countOfBytesClientExpectsToReceive = <# Received Bytes #>
        // Tasks are created in the suspended state.
        backgroundTask.resume()
        
    }
}
```
