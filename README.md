# azfLibrary
Open the Sandbox with in apps and many more features to help developers 

# informations
- First you need to download the library.
- add bundle library to conter file 
- like it ``` Depends: mobilesubstrate, co.azozzalfiras.azflibrary```

# Features:
- Get udid.
- Get model device.
- Import audio to Music app.
- Import video to Music app.
- Export link player video on safari.
- Features coming soon.


# Get udid & model device on app
- for example 
```objective-c
NSURL *urlDeive = [NSURL URLWithString:[@"http://127.0.0.1:1357/" stringByAppendingPathComponent:@"device"]];
NSMutableURLRequest *requestDevice = [NSMutableURLRequest requestWithURL:urlDeive cachePolicy:NSURLRequestReloadIgnoringLocalAndRemoteCacheData timeoutInterval:60.0];
[requestDevice setHTTPMethod:@"GET"];
NSData *receivedDataDevice = [NSURLConnection sendSynchronousRequest:requestDevice returningResponse:nil error:nil]?:[NSData data];
NSDictionary *jsonRespDevice = [NSJSONSerialization JSONObjectWithData:receivedDataDevice options:0 error:nil]?:@{};
NSString* udid = jsonRespDevice[@"udid"];
NSString* device = jsonRespDevice[@"device"];

if(udid && device){

// do something
}
```
