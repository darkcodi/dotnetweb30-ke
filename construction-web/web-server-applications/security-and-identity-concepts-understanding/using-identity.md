# Using identity

ASP.NET Core Identity is a membership system that adds **login functionality** to ASP.NET Core apps.

Identity can be configured using a SQL Server database to store user names, passwords, and profile data. Alternatively, another persistent store can be used, for example, Azure Table Storage.

Firstly, add these lines to `ConfigureServices`:

```csharp
services.AddDefaultIdentity<IdentityUser>()
    .AddDefaultUI(UIFramework.Bootstrap4)
    .AddEntityFrameworkStores<ApplicationDbContext>();

services.Configure<IdentityOptions>(options =>
{
    // Password settings.
    options.Password.RequireDigit = true;
    options.Password.RequireLowercase = true;
    options.Password.RequireNonAlphanumeric = true;
    options.Password.RequireUppercase = true;
    options.Password.RequiredLength = 6;
    options.Password.RequiredUniqueChars = 1;

    // Lockout settings.
    options.Lockout.DefaultLockoutTimeSpan = TimeSpan.FromMinutes(5);
    options.Lockout.MaxFailedAccessAttempts = 5;
    options.Lockout.AllowedForNewUsers = true;

    // User settings.
    options.User.AllowedUserNameCharacters =
    "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789-._@+";
    options.User.RequireUniqueEmail = false;
});

services.ConfigureApplicationCookie(options =>
{
    // Cookie settings
    options.Cookie.HttpOnly = true;
    options.ExpireTimeSpan = TimeSpan.FromMinutes(5);

    options.LoginPath = "/Identity/Account/Login";
    options.AccessDeniedPath = "/Identity/Account/AccessDenied";
    options.SlidingExpiration = true;
});
```

Also add this line before calling `UseMvc` in `Configure` method:

```csharp
app.UseAuthentication();
```

After that you can inject `SignInManager` and use it in your controllers:

```csharp
public async Task<IActionResult> OnPostAsync(string returnUrl = null)
{
    var user = new IdentityUser { UserName = Input.Email, Email = Input.Email };
    var result = await _userManager.CreateAsync(user, Input.Password);
    if (result.Succeeded)
    {
        _logger.LogInformation("User created a new account with password.");
        await _signInManager.SignInAsync(user, isPersistent: false);
        
        return LocalRedirect(returnUrl);
    }
    
    // If we got this far, something failed, redisplay form
    return Page();
}
```

