FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["Unattend.BackOffice.UI/Unattend.BackOffice.UI.csproj", "Unattend.BackOffice.UI/"]
RUN dotnet restore "Unattend.BackOffice.UI/Unattend.BackOffice.UI.csproj"
COPY . .
WORKDIR "/src/Unattend.BackOffice.UI"
RUN dotnet build "Unattend.BackOffice.UI.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "Unattend.BackOffice.UI.csproj" -c Release -o /app/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "Unattend.BackOffice.UI.dll"]
