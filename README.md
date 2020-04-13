# MVNet
- Supports a variety of proxies (Http/s, Socks4, Socks4a, Socks5).
- Supports TLS/SSL (tls1, tls1.1 tls1.2, tls1.3, SSL3.0).

## Features
#### HTTP Methods
- GET
- POST

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
