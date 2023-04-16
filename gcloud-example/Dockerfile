FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["gcloud-example.csproj", "gcloud-example/"]
RUN dotnet restore "gcloud-example/gcloud-example.csproj"
COPY . .
WORKDIR "/src/gcloud-example"
RUN dotnet build "gcloud-example.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "gcloud-example.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "gcloud-example.dll"]
