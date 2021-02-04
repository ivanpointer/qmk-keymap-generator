#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["PointerPlace.QMK.KeymapGenerator.Backend/PointerPlace.QMK.KeymapGenerator.Backend.csproj", "PointerPlace.QMK.KeymapGenerator.Backend/"]
RUN dotnet restore "PointerPlace.QMK.KeymapGenerator.Backend/PointerPlace.QMK.KeymapGenerator.Backend.csproj"
COPY . .
WORKDIR "/src/PointerPlace.QMK.KeymapGenerator.Backend"
RUN dotnet build "PointerPlace.QMK.KeymapGenerator.Backend.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "PointerPlace.QMK.KeymapGenerator.Backend.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "PointerPlace.QMK.KeymapGenerator.Backend.dll"]