# Web server implementations in ASP.NET Core

### Kestrel <a id="kestrel"></a>

{% hint style="info" %}
Kestrel is the **default** web server included in ASP.NET Core project templates.
{% endhint %}

Use Kestrel:

* By itself as an edge server processing requests directly from a network, including the Internet.

![](../../.gitbook/assets/image%20%28158%29.png)

* With a reverse proxy server, such as Internet Information Services \(IIS\), Nginx, or Apache.

![](../../.gitbook/assets/image%20%2861%29.png)

### HTTP.sys <a id="httpsys"></a>

If ASP.NET Core apps are run on Windows, HTTP.sys is an alternative to Kestrel. Kestrel is generally recommended for best performance. HTTP.sys can be used in scenarios where the app is exposed to the Internet and required capabilities are supported by HTTP.sys but not Kestrel.

![](../../.gitbook/assets/image%20%2885%29.png)

HTTP.sys can also be used for apps that are only exposed to an internal network.

![](../../.gitbook/assets/image%20%2850%29.png)

### Custom servers <a id="custom-servers"></a>

If the built-in servers don't meet the app's requirements, a custom server implementation can be created. The **Open Web Interface for .NET \(OWIN\)** guide demonstrates how to write a **Nowin-based IServer** implementation.

