# MISC INFO #

*LEARN NEW ANGULAR*:   angular.dev website – https://angular.dev/
 

   SHA256 = create hash; used to convert user passwords into a hash value before storing them in a database. The hash values are matched to the user's input during login verification.
https://emn178.github.io/online-tools/sha256.html
 
 
 
# TEST RestAPI within VSCode: #

   ThunderClient - Hand-crafted lightweight Rest Client for testing APIs. Supports collections, environments, git collaboration and local storage

   RESTClient - allows you to send HTTP request and view the response in Visual Studio Code directly
 
## Using REST Client:#

Add route.rest within your ROUTES folder to test your app routes (name whatever, as long as it ends in .rest or .http)

   [name].rest
 
Within route.rest:
 
   GET ALL:           
   Add Get request:  GET  http://localhost:[number]/[name]
 

Separate with ### to add new request
 
   GET ONE:         
   Add Get Request:  GET  http://localhost:[number]/[name]/[number/id]
 
 
 
Separate with ### to add new request
 
   Create One:    
   Add Post request:  POST http://localhost:[number]/[name]
   Content-Type: application/json
 
   {
      “name”:  “Amazing Person”,
      “subscribedToChannel”:  “Web Dev Simplified”
   }