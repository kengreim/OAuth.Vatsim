# OAuth.Vatsim

OAuth.Vatsim provides the security middleware to use [VATSIM Connect](https://vatsim.dev/api/connect-api) as an external login provider with ASP.NET Core applications. It borrows from the collection of other third-party providers: [AspNet.Security.OAuth.Providers](https://github.com/aspnet-contrib/AspNet.Security.OAuth.Providers).

# How to Use
The extension methods in this package are built for the ASP.NET Core builders.

An example usage, building on the .NET8 Blazor Web App template with Individual authentication and identity scaffolding, is:
```C#
builder.Services.AddAuthentication(options =>
    {
        options.DefaultScheme = IdentityConstants.ApplicationScheme;
        options.DefaultSignInScheme = IdentityConstants.ExternalScheme;
    })
    .AddVatsim(options =>
    {
        options.ClientId = CLIENT_ID_HERE;
        options.ClientSecret = CLIENT_SECRET_HERE;
    })
    .AddIdentityCookies();
```

# Defaults
The default provider uses the Vatsim Auth development endpoints. To change this, use `options.Server = VatsimAuthenticationServer.Production` in the options builder of the `AddVatsim` method.

By default, the handler requests the following scopes: `full_name`, `email`, `vatsim_details`, `country`.

On successful response, the user's VATSIM CID is mapped to `ClaimTypes.NameIdentifier`, full name is mapped to `ClaimTypes.Name` and email is mapped to `ClaimTypes.Email`


# Can I get it on NuGet?
Currently no, but I may contribute it to [AspNet.Security.OAuth.Providers](https://github.com/aspnet-contrib/AspNet.Security.OAuth.Providers) which is available on NuGet.
