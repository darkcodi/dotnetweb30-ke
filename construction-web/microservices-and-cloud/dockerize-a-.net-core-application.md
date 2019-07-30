# Dockerize a .NET Core application

## Dockerfile for an ASP.NET Core application

**Why build ASP.NET Core?**

* Open-source 
* Develop and run your ASP.NET Core apps cross-platform on Windows, MacOS, and Linux 
* Great for modern cloud-based apps, such as web apps, IoT apps, and mobile backends 
* ASP.NET Core apps can run on .NET Core or on the full .NET Framework 
* Designed to provide an optimized development framework for apps that are deployed to the cloud or run on-premises 
* Modular components with minimal overhead retain flexibility while constructing your solutions

**Create a Dockerfile for an ASP.NET Core application**

1. Create a Dockerfile in your project folder. 
2. Add the text below to your Dockerfile for either Linux or Windows Containers. The tags below are multi-arch meaning they pull either Windows or Linux containers depending on what mode is set in Docker Desktop for Windows. Read more on switching containers. 
3. The Dockerfile assumes that your application is called aspnetapp. Change the Dockerfile to use the DLL file of your project.

```text
FROM mcr.microsoft.com/dotnet/core/sdk:2.2 AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY *.csproj ./
RUN dotnet restore

# Copy everything else and build
COPY . ./
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:2.2
WORKDIR /app
COPY --from=build-env /app/out .
ENTRYPOINT ["dotnet", "aspnetapp.dll"]
```

1. To make your build context as small as possible add a .dockerignore file to your project folder and copy the following into it.

```text
bin\
obj\
```

**Build and run the Docker image**

1. Open a command prompt and navigate to your project folder. 
2. Use the following commands to build and run your Docker image:

```text
$ docker build -t aspnetapp .
$ docker run -d -p 8080:80 --name myapp aspnetapp
```

**View the web page running from a container**

* Go to localhost:8080 to access your app in a web browser. 
* If you are using the Nano Windows Container and have not updated to the Windows Creator Update there is a bug affecting how Windows 10 talks to Containers via “NAT” \(Network Address Translation\). You must hit the IP of the container directly. You can get the IP address of your container with the following steps:
  * Run docker inspect -f "" myapp 
  * Copy the container IP address and paste into your browser. \(For example, 172.16.240.197\)

