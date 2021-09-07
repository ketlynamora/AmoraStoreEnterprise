#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /src
COPY ["src/web/ASE.WebApp.MVC/ASE.WebApp.MVC.csproj", "src/web/ASE.WebApp.MVC/"]
RUN dotnet restore "src/web/ASE.WebApp.MVC/ASE.WebApp.MVC.csproj"
COPY . .
WORKDIR "/src/src/web/ASE.WebApp.MVC"
RUN dotnet build "ASE.WebApp.MVC.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "ASE.WebApp.MVC.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "ASE.WebApp.MVC.dll"]