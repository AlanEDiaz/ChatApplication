FROM mcr.microsoft.com/dotnet/core/aspnet:2.1-stretch-slim AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/core/sdk:2.1-stretch AS build
WORKDIR /src
COPY ["ChatTestApplication/ChatTestApplication.csproj", "ChatTestApplication/"]
RUN dotnet restore "ChatTestApplication/ChatTestApplication.csproj"
COPY . .
WORKDIR "/src/ChatTestApplication"
RUN dotnet build "ChatTestApplication.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "ChatTestApplication.csproj" -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "ChatTestApplication.dll"]