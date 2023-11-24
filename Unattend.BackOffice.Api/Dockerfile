FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["Unattend.BackOffice.Api/Unattend.BackOffice.Api.csproj", "Unattend.BackOffice.Api/"]
RUN dotnet restore "Unattend.BackOffice.Api/Unattend.BackOffice.Api.csproj"
COPY . .
WORKDIR "/src/Unattend.BackOffice.Api"
RUN dotnet build "Unattend.BackOffice.Api.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Unattend.BackOffice.Api.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Unattend.BackOffice.Api.dll"]
