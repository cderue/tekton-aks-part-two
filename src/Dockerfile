FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /src
COPY ["src/aspnetcoreapp.csproj", "src/"]
RUN dotnet restore "src/aspnetcoreapp.csproj"
COPY . .
WORKDIR "/src/src"
RUN dotnet build "aspnetcoreapp.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "aspnetcoreapp.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "aspnetcoreapp.dll"]
