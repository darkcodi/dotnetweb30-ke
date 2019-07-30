# Bundle and Minify assets

{% hint style="warning" %}
Bundling and minification are two **distinct** performance optimizations you can apply in a web app.
{% endhint %}

Used together, bundling and minification improve performance by reducing the number of server requests and reducing the size of the requested static assets.

Bundling and minification primarily **improve** the first page request **load time**.

### Bundling

{% hint style="success" %}
**Bundling** combines multiple files into a single file.
{% endhint %}

Bundling reduces the number of server requests that are necessary to render a web asset, such as a web page. You can create any number of individual bundles specifically for CSS, JavaScript, etc. Fewer files means fewer HTTP requests from the browser to the server or from the service providing your application. This results in improved first page load performance.

### Minification

{% hint style="success" %}
**Minification** removes unnecessary characters from code without altering functionality.
{% endhint %}

The result is a significant size reduction in requested assets \(such as CSS, images, and JavaScript files\). Common side effects of minification include shortening variable names to one character and removing comments and unnecessary whitespace.

### Impact of bundling and minification <a id="impact-of-bundling-and-minification"></a>

| Action | With B/M | Without B/M | Change |
| :--- | :--- | :--- | :--- |
| File Requests | 7 | 18 | 157% |
| KB Transferred | 156 | 264.68 | 70% |
| Load Time \(ms\) | 885 | 2360 | 167% |

### Build-time execution of B/M <a id="build-time-execution-of-bundling-and-minification"></a>

The **`BuildBundlerMinifier`** NuGet package enables the execution of bundling and minification at build time. The package injects MSBuild Targets which run at build and clean time. The _bundleconfig.json_ file is analyzed by the build process to produce the output files based on the defined configuration.

### Ad hoc execution of B/M <a id="ad-hoc-execution-of-bundling-and-minification"></a>

It's possible to run the bundling and minification tasks on an ad hoc basis, without building the project. Just add the `BundlerMinifier.Core` NuGet package to your project.

