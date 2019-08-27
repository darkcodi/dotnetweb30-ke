# IActionConstraint
The [HttpGet] Attribute and similar [Http-VERB] attributes implement IActionConstraint

Conceptually, IActionConstraint is a form of overloading, but instead of overloading methods with the same name, it's overloading between actions that match the same URL. Attribute routing also uses IActionConstraint and can result in actions from different controllers both being considered candidates.

You are responsible for implementing the Accept method and choosing an 'Order' for the constraint to execute. In this case, the Accept method returns true to denote the action is a match when the country route value matches. This is different from a RouteValueAttribute in that it allows fallback to a non-attributed action. The sample shows that if you define an en-US action then a country code like fr-FR will fall back to a more generic controller that doesn't have [CountrySpecific(...)] applied.
```csharp
public class CountrySpecificAttribute : Attribute, IActionConstraint
{
    private readonly string _countryCode;

    public CountrySpecificAttribute(string countryCode)
    {
        _countryCode = countryCode;
    }

    public int Order
    {
        get
        {
            return 0;
        }
    }

    public bool Accept(ActionConstraintContext context)
    {
        return string.Equals(
            context.RouteContext.RouteData.Values["country"].ToString(),
            _countryCode,
            StringComparison.OrdinalIgnoreCase);
    }
}
```

The Order property decides which stage the constraint is part of. Action constraints run in groups based on the Order. For example, all of the framework provided HTTP method attributes use the same Order value so that they run in the same stage. You can have as many stages as you need to implement your desired policies.
