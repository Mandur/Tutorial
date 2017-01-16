#1
Follow the tutorial [here](https://docs.microsoft.com/en-us/dotnet/articles/core/tutorials/using-with-xplat-cli) to install the .NET cli.

#2
Create an Aspnet project as described [here](https://docs.microsoft.com/en-us/aspnet/core/getting-started)

#2'(Optional)
Install (VSCode)[https://code.visualstudio.com/] as a code editor on Linux

#3
Open the project by typing ```code .``` in your command line

#4 
Edit the file Startup.cs and comment the following lines in the Configure method (this will allow error message to display on the browser even locally)

```cs
  // if (env.IsDevelopment())
            // {
                app.UseDeveloperExceptionPage();
                 app.UseDatabaseErrorPage();
                app.UseBrowserLink();
            // }
            // else
            // {
            //     app.UseExceptionHandler("/Home/Error");
            // }
```

#5
create a new model in the Models folder named ```Person.cs```. (In VSCode, right click on the folder and create a new file). We would like to generate a CRUD like system to manage these persons now.

```cs
namespace WebApplication.Models
{
    public class Person
    {
        public int Id {get; set;}

        public string Name {get; set;}

        public int Age {get; set;}
    }
}

```

#6
Update the file project.json to the latest version by replacing its content by the following: (This is an update to the package to ensure they work with the latest version)
```json
{
  "userSecretsId": "aspnet-WebApplication-0799fe3e-6eaf-4c5f-b40e-7c6bfd5dfa9a",

  "dependencies": {
    "Microsoft.NETCore.App": {
      "version": "1.1.0",
      "type": "platform"
    },
    "Microsoft.AspNetCore.Authentication.Cookies": "1.1.0",
    "Microsoft.AspNetCore.Diagnostics": "1.1.0",
    "Microsoft.AspNetCore.Diagnostics.EntityFrameworkCore": "1.1.0",
    "Microsoft.AspNetCore.Identity.EntityFrameworkCore": "1.1.0",
    "Microsoft.AspNetCore.Mvc": "1.1.0",
    "Microsoft.AspNetCore.Razor.Tools": {
      "version": "1.1.0-preview4-final",
      "type": "build"
    },
    "Microsoft.AspNetCore.Routing": "1.1.0",
    "Microsoft.AspNetCore.Server.IISIntegration": "1.1.0",
    "Microsoft.AspNetCore.Server.Kestrel": "1.1.0",
    "Microsoft.AspNetCore.StaticFiles": "1.1.0",
    "Microsoft.EntityFrameworkCore.Sqlite": "1.1.0",
    "Microsoft.EntityFrameworkCore.Tools": {
      "version": "1.1.0-preview4-final",
      "type": "build"
    },
    "Microsoft.Extensions.Configuration.EnvironmentVariables": "1.1.0",
    "Microsoft.Extensions.Configuration.Json": "1.1.0",
    "Microsoft.Extensions.Configuration.UserSecrets": "1.1.0",
    "Microsoft.Extensions.Logging": "1.1.0",
    "Microsoft.Extensions.Logging.Console": "1.1.0",
    "Microsoft.Extensions.Logging.Debug": "1.1.0",
    "Microsoft.VisualStudio.Web.BrowserLink.Loader": "14.1.0",
    "Microsoft.EntityFrameworkCore.Sqlite.Design":"1.1.0",
    "Microsoft.VisualStudio.Web.CodeGeneration.Tools": {
      "version": "1.1.0-preview4-final",
      "type": "build"
    },
    "Microsoft.VisualStudio.Web.CodeGenerators.Mvc": {
      "version": "1.1.0-preview4-final",
      "type": "build"
    }
  },

  "tools": {
    "Microsoft.AspNetCore.Razor.Tools": {
      "version": "1.1.0-preview4-final",
      "imports": "portable-net45+win8+dnxcore50"
    },
    "Microsoft.AspNetCore.Server.IISIntegration.Tools": {
      "version": "1.1.0-preview4-final",
      "imports": "portable-net45+win8+dnxcore50"
    },
    "Microsoft.EntityFrameworkCore.Tools.DotNet": {
      "version": "1.1.0-preview4-final",
      "imports": [
        "portable-net45+win8+dnxcore50",
        "portable-net45+win8"
      ]
    },
    "Microsoft.Extensions.SecretManager.Tools": {
      "version": "1.1.0-preview4-final",
      "imports": "portable-net45+win8+dnxcore50"
    },
    "Microsoft.VisualStudio.Web.CodeGeneration.Tools": {
      "version": "1.1.0-preview4-final",
      "imports": [
        "portable-net45+win8+dnxcore50",
        "portable-net45+win8"
      ]
    }
  },

  "frameworks": {
    "netcoreapp1.1": {
      "imports": [
        "dotnet5.6",
        "dnxcore50",
        "portable-net45+win8"
      ]
    }
  },

  "buildOptions": {
    "debugType": "portable",
    "emitEntryPoint": true,
    "preserveCompilationContext": true
  },

  "runtimeOptions": {
    "configProperties": {
      "System.GC.Server": true
    }
  },


  "publishOptions": {
    "include": [
      "wwwroot",
      "**/*.cshtml",
      "appsettings.json",
      "web.config"
    ]
  },

  "scripts": {
    "prepublish": [ "npm install", "bower install", "gulp clean", "gulp min" ],
    "postpublish": [ "dotnet publish-iis --publish-folder %publish:OutputPath% --framework %publish:FullTargetFramework%" ]
  },

  "tooling": {
    "defaultNamespace": "WebApplication"
  }
}

```
#7 
Go back to the command line and write the line. This will update the package you described in the package.json file.
```
dotnet restore
```

#8 
Based on the model Person.cs you created in the previous steps, we would like to scaffold a controller and a link to the DB. To create this, go to your command line interface and write the following command

```
dotnet aspnet-codegenerator controller –force --controllerName PeopleController --model WebApplication.Models.Person --dataContext ApplicationDbContext --relativeFolderPath Controllers --referenceScriptLibraries --useDefaultLayout
```

#9
Go check the new PeopleController file located in the Controllers folder, you will se the generated scaffolded controller. Also check the ApplicationDBContext class in Models/Data, you will see the line
```
 public DbSet<Person> Person { get; set; }
 ```
 this is the declared link generated by the scaffolding tool between the DB and the code.

#10
In order to add the Person class to the database please write the following command in the database

```
dotnet ef migrations add
dotnet ef database update
```

#11 
Run the Website.

#12 Optional
Build a dockerfile, (https://stormpath.com/blog/tutorial-deploy-asp-net-core-on-linux-with-docker)
publish it to the dockerhub(https://docs.docker.com/engine/tutorials/dockerrepos/) and publish it to the Web app for Linux on Azure.

