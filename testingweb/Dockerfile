FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 5000

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY ["testingweb.csproj", "."]
RUN dotnet restore "testingweb.csproj"
COPY . .
WORKDIR "/src"
RUN dotnet build "testingweb.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "testingweb.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENV ASPNETCORE_URLS=http://+:5000
ENTRYPOINT ["dotnet", "testingweb.dll"]
