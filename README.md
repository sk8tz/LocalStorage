# Blazored LocalStorage
A library to provide access to local storage in Blazor applications

[![Build Status](https://dev.azure.com/blazored/LocalStorage/_apis/build/status/Blazored.LocalStorage?branchName=master)](https://dev.azure.com/blazored/LocalStorage/_build/latest?definitionId=1&branchName=master)

![Nuget](https://img.shields.io/nuget/v/blazored.localstorage.svg)

## Important Notice For ASP.NET Core Razor Components Apps
There is currently an issue with [ASP.NET Core Razor Components apps](https://devblogs.microsoft.com/aspnet/aspnet-core-3-preview-2/#sharing-component-libraries) (not Blazor). They are unable to import static assets from component libraries such as this one. 

You can still use this package, however, you will need to manually add the JavaScript file to your Razor Components `wwwroot` folder. Then you will need to reference it in your `index.html`.

Alternativly, there is a great package by [Mister Magoo](https://github.com/SQL-MisterMagoo/BlazorEmbedLibrary) which offers a solution to this problem without having to manually copy files.

### Installing

You can install from Nuget using the following command:

`Install-Package Blazored.LocalStorage`

Or via the Visual Studio package manger.

### Setup

First, you will need to register local storage with the service collection in your _startup.cs_ file

```c#
public void ConfigureServices(IServiceCollection services)
{
    services.AddBlazoredLocalStorage();
}
``` 

### Usage
This is an example of using local storage in a .cshtml file 

```c#
@inject Blazored.LocalStorage.ILocalStorageService localStorage

@functions {

    protected override async Task OnInitAsync()
    {
        await localStorage.SetItem("name", "John Smith");
        var name = await localStorage.GetItem<string>("name");
    }

}
```

The APIs available are
 - SetItem()
 - GetItem()
 - RemoveItem()
 - Clear()
 - Length()
 - Key()

 **All APIs are now _async_**

**Note:** Blazored.LocalStorage methods will handle the serialisation and de-serialisation of the data for you.
