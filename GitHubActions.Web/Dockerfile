FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build
WORKDIR /src
COPY ["GitHubActions.Web/GitHubActions.Web.csproj", "GitHubActions.Web/"]
RUN dotnet restore "GitHubActions.Web/GitHubActions.Web.csproj"
COPY . .
WORKDIR "/src/GitHubActions.Web"
RUN dotnet build "GitHubActions.Web.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "GitHubActions.Web.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "GitHubActions.Web.dll"]
