#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/core/aspnet:2.2-stretch-slim AS build
WORKDIR /src
COPY ["BulletinBoard/BulletinBoard.csproj", "BulletinBoard/"]
RUN dotnet restore "BulletinBoard/BulletinBoard.csproj"
COPY . .
WORKDIR "/src/BulletinBoard"
RUN dotnet build "BulletinBoard.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "BulletinBoard.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "BulletinBoard.dll"]



