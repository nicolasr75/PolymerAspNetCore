# Polymer with ASP.NET Core 2.0

This demo shows how to connect the default template for an ASP.NET Core 2.0 Web Api and the simple Polymer application template.

It emerged from a discussion about optimizing the build chain for apps that use both Polymer and ASP.NET Core 2.0 here:
https://stackoverflow.com/questions/42823951/publishing-polymer-asp-net-core/42857870#42857870

It uses a batch file (polymer-build.cmd) for building the Polymer app. This batch file is launched from the *before publish* target. See PolymerAspNetCore.csproj!
The wwwroot directory is excluded from the default publishing because after polymer build has been executed, only the content of the build output should be copied to the publish directory.
This is achieved using an *after publish* target.

Note that this demo uses the *es6-unbundled* Polymer build preset (see polymer.json). If you want another preset or custom settings you also need to change the path in the *clientfiles* tag in the csproj file!

The only thing that has been changed in the ASP.NET Core code is that Startup.cs contains these to extra lines to server the Polymer files
```
app.UseDefaultFiles();
app.UseStaticFiles();
```

To publish the entire app use the *Publish* command from the context menu of the project. By default the publish directory is located in the bin/Release directory.

To test the published app open a console in the publish directory and execute `dotnet PolymerAspNetCore.dll`.