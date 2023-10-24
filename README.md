# webapi-versoning

In ASP.NET Core, you can implement API versioning using different controllers for different API versions. This allows you to maintain multiple versions of the same API in separate controllers, making it easier to manage and maintain backward compatibility. Here's how you can achieve this:

Step 1: Install Microsoft.AspNetCore.Mvc.Versioning Package
First, ensure you have the Microsoft.AspNetCore.Mvc.Versioning NuGet package installed. You can install it using the following command in the Package Manager Console:

bash
Copy code
Install-Package Microsoft.AspNetCore.Mvc.Versioning
Step 2: Configure API Versioning in Startup.cs
In your Startup.cs file, configure API versioning by adding the following code to the ConfigureServices method:

csharp
Copy code
services.AddApiVersioning(options =>
{
    options.DefaultApiVersion = new ApiVersion(1, 0);
    options.AssumeDefaultVersionWhenUnspecified = true;
    options.ReportApiVersions = true;
});
This code configures API versioning with the default version set to 1.0 and enables API version reporting.

Step 3: Create Versioned Controllers
Create multiple controllers for different API versions. For example, if you want versions 1.0 and 2.0, you can create controllers named V1Controller and V2Controller:

csharp
Copy code
[ApiVersion("1.0")]
[Route("api/v{version:apiVersion}/[controller]")]
public class V1Controller : ControllerBase
{
    [HttpGet]
    public IActionResult Get()
    {
        return Ok("Version 1.0");
    }
}

[ApiVersion("2.0")]
[Route("api/v{version:apiVersion}/[controller]")]
public class V2Controller : ControllerBase
{
    [HttpGet]
    public IActionResult Get()
    {
        return Ok("Version 2.0");
    }
}
In these controllers, the [ApiVersion] attribute is used to specify the API version associated with each controller. The version parameter in the route template [Route("api/v{version:apiVersion}/[controller]")] ensures that the correct versioned controller is invoked based on the API version specified in the request URL.

Step 4: Test the API Versions
Now, you can test your API versions using the following URLs:

http://localhost:5000/api/v1/v1: This will invoke the Get action in the V1Controller.
http://localhost:5000/api/v2/v2: This will invoke the Get action in the V2Controller.
By following these steps, you can maintain multiple versions of the same API using different controllers in ASP.NET Core. This approach allows for better organization and separation of concerns, making it easier to manage and extend your API in the future.
