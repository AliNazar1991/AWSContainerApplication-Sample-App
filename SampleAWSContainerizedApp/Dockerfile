FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY SampleAWSContainerizedApp/SampleAWSContainerizedApp.csproj SampleAWSContainerizedApp/
RUN dotnet restore SampleAWSContainerizedApp/SampleAWSContainerizedApp.csproj
COPY . .
WORKDIR /src/SampleAWSContainerizedApp
RUN dotnet build SampleAWSContainerizedApp.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish SampleAWSContainerizedApp.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "SampleAWSContainerizedApp.dll"]
