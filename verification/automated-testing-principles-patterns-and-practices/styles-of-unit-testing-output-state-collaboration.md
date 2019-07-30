# Styles of Unit Testing \(Output / State / Collaboration\)

There are 3 major styles of unit testing:

* Output verification
* State verification
* Collaboration verification

### Output verification

{% hint style="success" %}
You pass some input to the system under test and **check what output** it produces.
{% endhint %}

![](../../.gitbook/assets/image%20%286%29.png)

The yellow line here shows the point at which the examination is done.

In order to apply this style of unit testing, the system under test must not change global or internal state, so that the only component to verify would be its return value. This style of unit testing is also known as functional style. The "sut" method here doesn't leave any side effects and doesn't refer to the external world, its inputs and outputs are fully encoded with its method signature.

### State verification

{% hint style="success" %}
You **verify the state** of the system after the operation is completed.
{% endhint %}

![](../../.gitbook/assets/image%20%28107%29.png)

The yellow circles on this picture represent that final state.

Unlike the previous sample, this method doesn't return any value, its outcome is the change made to its internal state.

### Collaboration verification

{% hint style="success" %}
You check that **all collaborators got invoked** in a correct order and with correct parameters.
{% endhint %}

![](../../.gitbook/assets/image%20%2893%29.png)

This is normally done by substituting the collaborators with test doubles, such as **mocks**. For example, we create a fake implementation of the `IDatabase` interface which we then pass to the service. After that, the test verifies that the expected method was called and then the correct parameter was used.

