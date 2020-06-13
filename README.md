# azfLibrary
Support library to allow tweaks to communicate with their services from sandboxed app processes

# informations
- First you need to download the library.
- add bundle library to conter file 
- like it ``` Depends: mobilesubstrate, co.azozzalfiras.azflibrary```
- you can see library on Pakcix 
- https://repo.packix.com/package/co.azozzalfiras.azflibrary/

# Features:
- Get udid.
- Get model device.
- Import audio to Music app.
- Import video to Music app.
- Export link player video on safari.
- Save photos to the photo album application.
- Save videos to the photo album application.
- Create files inside applications.
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


# Import video & audio to Music App
- for example 
```objective-c

NSString *pathAuido = @"/var/azfLibrary/audio.m4a";
NSString *imageAuido = @"/var/azfLibrary/audio.png"
NSURL *url = [NSURL URLWithString:@"http://127.0.0.1:1357/"];
NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url cachePolicy:NSURLRequestReloadIgnoringLocalAndRemoteCacheData timeoutInterval:60.0];
[request setHTTPMethod:@"POST"];
[request setHTTPBody:[NSJSONSerialization dataWithJSONObject:@{@"path": pathAuido?:@"",	@"metadata": imageAuido?:@""} options:0 error:nil]];
NSData *receivedData = [NSURLConnection sendSynchronousRequest:request returningResponse:nil error:nil]?:[NSData data];
NSDictionary *jsonResp = [NSJSONSerialization JSONObjectWithData:receivedData options:0 error:nil]?:@{};
if([jsonResp[@"status"]?:@NO boolValue]) {
// imported
} else {
// Import Failed
}
```


# Export link player video on safari
- for example 
```objective-c

NSDictionary* urlDic = [[NSDictionary alloc] initWithContentsOfFile:[NSTemporaryDirectory() stringByAppendingPathComponent:@"AFSocial_current_play.link"]]?:@{};
NSString* mediaURLSt = urlDic[@"url"];
NSString* filename = [NSString stringWithFormat:@"%@", [[NSURL URLWithString:mediaURLSt?:@""] lastPathComponent]];
NSLog(@"%@",filename);
```

# Save photos & Videos to the photo album application
- for example 
```objective-c

// this path for save
NSString *pathFileVideo = @"/var/azfLibrary/Video.mp4";

// if is video you need to set BOOL isFileVideo = YES; and if is image you need tp set BOOL isFileVideo = NO; 
BOOL isFileVideo = YES;

NSURL *url = [NSURL URLWithString:[@"http://127.0.0.1:1357/" stringByAppendingPathComponent:@"cameraImport"]];
NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url cachePolicy:NSURLRequestReloadIgnoringLocalAndRemoteCacheData timeoutInterval:60.0];
[request setHTTPMethod:@"POST"];
[request setHTTPBody:[NSJSONSerialization dataWithJSONObject:@{@"path": pathFileVideo?:@"", @"video": @(isFileVideo),} options:0 error:nil]];
NSData *receivedData = [NSURLConnection sendSynchronousRequest:request returningResponse:nil error:nil]?:[NSData data];
NSDictionary *jsonResp = [NSJSONSerialization JSONObjectWithData:receivedData options:0 error:nil]?:@{};

if([jsonResp[@"status"]?:@NO boolValue]) {
// saved
} else {
// save failed
}


```




# Create files inside applications
- for example 
```objective-c

// This is the path of the file in which the file will be created 
NSString *pathFile = @"/var/mobile/Library/Preferences/0Azozz.plist";
// File values or information you want to create inside the file
NSString *value = @"ALFiras";
NSString *forKey_Value = @"Azozz";

NSURL *url = [NSURL URLWithString:[@"http://127.0.0.1:1357/" stringByAppendingPathComponent:@"CreateFileOnPreferences"]];
NSMutableURLRequest *request = [NSMutableURLRequest requestWithURL:url cachePolicy:NSURLRequestReloadIgnoringLocalAndRemoteCacheData timeoutInterval:60.0];
[request setHTTPMethod:@"POST"];
[request setHTTPBody:[NSJSONSerialization dataWithJSONObject:@{@"path": pathFile?:@"", @"value" : value?:@"", @"forKey_Value" : forKey_Value?:@"",} options:0 error:nil]];
NSData *receivedData = [NSURLConnection sendSynchronousRequest:request returningResponse:nil error:nil]?:[NSData data];
NSDictionary *jsonResp = [NSJSONSerialization JSONObjectWithData:receivedData options:0 error:nil]?:@{};


if([jsonResp[@"status"]?:@NO boolValue]) {

// file was created

} else {
// Create  file failed
}

```

# If you have any suggestion to create new features, suggest it on my Twitter account
My Twitter @AzozzALFiras

https://twitter.com/AzozzALFiras

 

