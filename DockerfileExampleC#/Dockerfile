FROM mcr.microsoft.com/dotnet/aspnet:3.1 AS base

ENV TZ='Europe/Brussels'

EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:3.1 AS build
WORKDIR /api
COPY ["Service/projectName/projectName.csproj", "Service/projectName/"]
RUN dotnet restore "Service/projectName/projectName.csproj"
COPY . .
WORKDIR "/api/Service/projectName"

RUN dotnet build "projectName.csproj" -c Release -o /api/build

FROM build AS publish
RUN dotnet publish "projectName.csproj" -c Release -o /api/publish /p:UseAppHost=false

FROM base AS final
WORKDIR /api
COPY --from=publish /api/publish .
COPY ./Service/projectName/Assets ./Assets
RUN mkdir Tmp

ENTRYPOINT ["dotnet", "projectName.dll"]
