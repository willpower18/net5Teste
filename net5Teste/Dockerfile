#See https://aka.ms/containerfastmode to understand how Visual Studio uses this Dockerfile to build your images for faster debugging.

FROM mcr.microsoft.com/dotnet/aspnet:5.0-buster-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:5.0-buster-slim AS build
WORKDIR /src
COPY ["net5Teste/net5Teste.csproj", "net5Teste/"]
RUN dotnet restore "net5Teste/net5Teste.csproj"
COPY . .
WORKDIR "/src/net5Teste"
RUN dotnet build "net5Teste.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "net5Teste.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "net5Teste.dll"]