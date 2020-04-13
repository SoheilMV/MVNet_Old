# [Download](https://github.com/SoheilMV/MVNet/blob/master/MVNet.zip)

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
- POST

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
#### How To Request
````csharp
var hr = new HttpRequest();

// Get
var res = hr.Get("https://...");

// Get Async
var res = await hr.GetAsync("https://...");

// Post
var res = hr.Post("https://...", "name1=value1&name2=value2"); //Default ContentType is "application/x-www-form-urlencoded"

// Post
var res = hr.Post("https://...", "name1=value1&name2=value2", "application/x-www-form-urlencoded");

// Post Async
var res = await hr.Post("https://...", "name1=value1&name2=value2"); //Default ContentType is "application/x-www-form-urlencoded"

// Post Async
var res = await hr.Post("https://...", "name1=value1&name2=value2", "application/x-www-form-urlencoded");
````

#### SSL(ON/OFF)
```csharp
//ON
var hr = new HttpRequest()
{
    Ssl = true
};

//OFF
var hr = new HttpRequest()
{
    Ssl = false
};
```

#### Set Proxy
````csharp
ProxyClient pc = new ProxyClient(ProxyType.Http, "127.0.0.1:80");
//Or
ProxyClient pc = new ProxyClient(ProxyType.Http, "127.0.0.1", 80);
//Or
ProxyClient pc = new ProxyClient(ProxyType.Http, "127.0.0.1", 80, "User", "Pass");

var hr = new HttpRequest()
{
    UseProxy = true,
    ProxyClient = pc
};
````

#### Set Proxy Authentication
````csharp
ProxyClient pc = new ProxyClient(ProxyType.Http, "127.0.0.1:80");

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
string cookie;
res.Cookies.TryGetValue("name", out cookie);
````

#### Get Header
````csharp
string header;
res.Headers.TryGetValue("name", out cookie);
````
