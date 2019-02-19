#Depending on the operating system of the host machines(s) that will build or run the containers, the image specified in the FROM statement may need to be changed.
#For more information, please see https://aka.ms/containercompat

FROM microsoft/aspnetcore-build:2.0 AS base
WORKDIR /app
EXPOSE 59308
EXPOSE 44321

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY . WebApplication1/
RUN dotnet restore "WebApplication1/AzureKVault.csproj"
COPY . .
WORKDIR /src/WebApplication1
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "AzureKVault.dll"]