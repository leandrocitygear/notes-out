FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build
WORKDIR /src

COPY ["notes-out.ApiService/notes-out.ApiService.csproj", "notes-out.ApiService/"]
COPY ["notes-out.ServiceDefaults/notes-out.ServiceDefaults.csproj", "notes-out.ServiceDefaults/"]

RUN dotnet restore "notes-out.ApiService/notes-out.ApiService.csproj"

COPY . .

WORKDIR "/src/notes-out.ApiService"
RUN dotnet publish "notes-out.ApiService.csproj" \
    -c Release \
    -o /app/publish \
    --no-restore

FROM mcr.microsoft.com/dotnet/aspnet:10.0 AS final
WORKDIR /app

COPY --from=build /app/publish .

ENV ASPNETCORE_URLS=http://+:8080

EXPOSE 8080

ENTRYPOINT ["dotnet", "notes-out.ApiService.dll"]