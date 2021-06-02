FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["SimpleChat.App/SimpleChat.App.csproj", "SimpleChat.App/"]
RUN dotnet restore "SimpleChat.App/SimpleChat.App.csproj"
COPY . .
WORKDIR "/src/SimpleChat.App"
RUN dotnet build "SimpleChat.App.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "SimpleChat.App.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "SimpleChat.App.dll"]
