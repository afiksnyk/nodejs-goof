FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["NuGet.Config", ""]
COPY ["DGT.Api.Azure.Ext.HealthManagerV6.csproj", ""]
RUN dotnet restore "./DGT.Api.Azure.Ext.HealthManagerV6.csproj"
COPY . .
WORKDIR "/src/."
RUN dotnet build "DGT.Api.Azure.Ext.HealthManagerV6.csproj" -c Release -o /app/build
 
FROM build AS publish
RUN dotnet publish "DGT.Api.Azure.Ext.HealthManagerV6.csproj" -c Release -o /app/publish
 
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "DGT.Api.Azure.Ext.HealthManagerV6.dll"]
