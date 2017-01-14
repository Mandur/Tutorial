#1
Follow the tutorial [here](https://docs.microsoft.com/en-us/dotnet/articles/core/tutorials/using-with-xplat-cli) to install the .NET cli.

#2
Create an Aspnet project as described [here](https://docs.microsoft.com/en-us/aspnet/core/getting-started)

#3
Open the project by typing '''code .''' in your command line

#4 
Edit the file Startup.cs and comment the following lines in the Configure method 

'''csharp
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
'''

create a new model in Models folder named Person.cs 

Update project.json

dotnet aspnet-codegenerator controller –force --controllerName PeopleController --model WebApplication.Models.Person --dataContext ApplicationDbContext --relativeFolderPath Controllers --referenceScriptLibraries --useDefaultLayout

dotnet ef migrations add

dotnet ef database update

Create a linux web app

Follow this

https://docs.microsoft.com/en-us/azure/app-service-web/app-service-deploy-local-git


