#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/sdk:3.1-buster AS build
WORKDIR /src
COPY ["Server/test.Server.csproj", "Server/"]
COPY ["Client/test.Client.csproj", "Client/"]
COPY ["Shared/test.Shared.csproj", "Shared/"]
RUN dotnet restore "Server/test.Server.csproj"
COPY . .
WORKDIR "/src/Server"
RUN dotnet build "test.Server.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "test.Server.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "test.Server.dll"]