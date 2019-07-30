# Testing Pyramid, Agile Testing Pyramid, Diamond

### Traditional pyramid

![](../../.gitbook/assets/image%20%28127%29.png)

In the traditional view, most if not all of the effort was in developing UI-centric functional tests that explored the application via the GUI. There might be some lower-level tests and a few unit tests, but teams mostly staid at the upper tier.

### Agile Testing Pyramid

![](../../.gitbook/assets/image%20%28137%29.png)

The agile test automation pyramid is a strategy that attempts to turn all of this around–literally.

Instead of the testers being responsible for testing AND writing all of the test automation, it becomes a whole-team responsibility. The developers take most of the ownership for unit-level automation, but testers can operate here as well. The upper tier focuses on limited UI-based automation. Usually, these are longer running, core customer usage workflows that are best implemented at this level.

### Ice-cream cone anti-pattern

![](../../.gitbook/assets/image%20%28108%29.png)

### Testing diamond

![](../../.gitbook/assets/image%20%28164%29.png)

While it is certainly true that integration tests are more costly than unit tests, it is also true that integration is the place where the real business value is. Unit tests are often insufficient. The nature of the engineering simulation problem that we were solving is such that the solution of the whole system of equations is necessary to see the full interplay of the complex physics being simulated. Unit tests cannot easily handle issues associated with round off or approximation methods.

