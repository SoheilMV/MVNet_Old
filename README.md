# MVNet
#### Supports TLS/SSL 
- tls 1.0
- tls 1.1
- tls 1.2
- tls 1.3
- SSL 3.0

#### Supports a variety of proxies
- Http/s
- Socks4
- Socks4a
- Socks5

#### Supports Proxy Authentication
- Basic Authentication
- Digest Authentication
- Windows NT Challenge/Response authentication (ntlm)

#### HTTP Methods
- GET
- HEAD
- OPTIONS
- DELETE
- POST
- PUT
- PATCH

## Features
#### Using
```csharp
using MVNet;

try
{
    var hr = new HttpRequest();
    var res = hr.Get("https://api.ipify.org?format=json");
    if (res.IsOk)
    {
        Console.WriteLine(res.Content);
    }
    else
    {
        Console.WriteLine(res.StatusCode);
    }
}
catch (HttpException ex)
{
    Console.WriteLine(ex.Message);
}
```

#### How to use StringContent
```csharp
StringContent content = new StringContent();
content.ContentType = "contenttype"; //Default is application/x-www-form-urlencoded
content["name1"] = "value1";
content["name2"] = "value2";

//Or

StringContent content = new StringContent("queryparams", "contenttype", encode);
```

#### How to use MultipartContent
```csharp
MultipartContent content = new MultipartContent(); //Generate random boundary
//Or
MultipartContent content = new MultipartContent("boundary");

content.AddParam("name", "value");
content.AddParam("name", "filename", "contenttype");
```

#### How to use StreamContent
```csharp
StreamContent content = new StreamContent(stream); //Default ContentType is application/x-www-form-urlencoded
//Or
StreamContent content = new StreamContent(stream, contentType);
//Or
StreamContent content = new StreamContent(stream, contentType, size);
```

#### Ssl Accept All Certificates(ON/OFF)
```csharp
//ON
var hr = new HttpRequest()
{
    AcceptAllCert = true
};

//OFF
var hr = new HttpRequest()
{
    AcceptAllCert = false
};
```

#### Set Proxy
````csharp
ProxyClient pc = new ProxyClient(type, "host:port");
//Or
ProxyClient pc = new ProxyClient(type, "host", port);
//Or
ProxyClient pc = new ProxyClient(type, "host", port, "user", "pass");

var hr = new HttpRequest()
{
    Proxy = pc
};

//Or

var hr = new HttpRequest()
{
    Proxy = ProxyClient.Parse(type, "host:port");
};
````

#### Set Proxy Authentication
````csharp
ProxyClient pc = new ProxyClient(type, "host:port");

pc.ProxyAuthentication = ProxyAuthentication.Basic;
//Or
pc.ProxyAuthentication = ProxyAuthentication.Digest;
//Or
pc.ProxyAuthentication = ProxyAuthentication.Ntlm;
````

#### Set Cookie
```csharp
CookieDictionary cookie = new CookieDictionary();
cookie.Add("name1", "value1");
cookie.Add("name2", "value2");

var hr = new HttpRequest()
{
    Cookies = cookie
};

//Or

var hr = new HttpRequest();
hr.Cookies.Add("name1", "value1");
hr.Cookies.Add("name2", "value2");
```

#### Set Header
```csharp
HeaderDictionary header = new HeaderDictionary();
header.Add("name1", "value1");
header.Add("name2", "value2");

var hr = new HttpRequest()
{
    Headers = header
};

//Or

var hr = new HttpRequest();
hr.Headers.Add("name1", "value1");
hr.Headers.Add("name2", "value2");
```

#### Get Cookies
````csharp
string cookie = res.GetCookie("name");
````

#### Get Header
````csharp
string header = res.GetHeader("name");
````
