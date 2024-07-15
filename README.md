How it Works:
Create a new ASP .Net MVC template

Step1: 

* Rigt Click on Project ( Go to Add, New Scaffolded item and Select item, Override all files)
* Select Data Context Class and Click on Add button.

Step 2:

* Go to appsettings.json
* change the default server to local name,
*  "ConnectionStrings": {
    "DefaultConnection": "Server=pramod;Database=GoogleAuthDemoDb;Trusted_Connection=True;MultipleActiveResultSets=true;TrustServerCertificate=True"
  },
* Add-Migration
* Update-Database

Step 3:

* Go to https://console.cloud.google.com/apis/library and Create a new Project
* Go to API & Services
* Select OAuth Consent Screen Select External and Create
* Select Credentials fill the form, we have to authorized redirect URIs ,in this app case (https://localhost:7295/signin-google) and click on create
* Credential will be created.

Step 4:
since, it is sensetive information, we will not keeping it in the appsettings.json , when you do it in server , you should store it in some kind of app vault for eg.(ENV_VARIABLE)

For this testing/development  purpose, we will be storing it in the appsecret;

* Go to View and Select Terminal
* Change the directory cd googleauthdemo
* dotnet user-secrets set "Authentication:Google:ClientId:" "326966679555-hjiovgusdc3k9v1nt37qtvucm5en1c83.apps.googleusercontent.com"
* dotnet user-secrets set "Authentication:Google:ClientSecret:" "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"
* Add package: install-package Microsoft.AspNetCore.Authentication.Google

Step 5:
Go to Program.cs
and Add the authentication for google:
builder.Services.AddAuthentication().AddGoogle(googleOptions =>
{
    googleOptions.ClientId = configuration["Authentication:Google:ClientId"];
    googleOptions.ClientSecret = configuration["Authentication:Google:ClientSecret"];
});

* Go to HomeController and add [Authorize] attribute to the privacy action to test the authorization
* Run the app and test the applicaiton.







