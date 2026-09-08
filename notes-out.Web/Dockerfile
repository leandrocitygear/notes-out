FROM mcr.microsoft.com/dotnet/sdk:10.0 AS build

WORKDIR /src

COPY ["notes-out.Web/notes-out.Web.csproj", "notes-out.Web/"]
COPY ["notes-out.ServiceDefaults/notes-out.ServiceDefaults.csproj", "notes-out.ServiceDefaults/"]

RUN dotnet restore "notes-out.Web/notes-out.Web.csproj"

COPY . .

WORKDIR "/src/notes-out.Web"

RUN dotnet publish "notes-out.Web.csproj" \
    -c Release \
    -o /app/publish \
    --no-restore

FROM mcr.microsoft.com/dotnet/aspnet:10.0 AS final

WORKDIR /app

COPY --from=build /app/publish .

ENV ASPNETCORE_URLS=http://+:8080

EXPOSE 8080

ENTRYPOINT ["dotnet", "notes-out.Web.dll"]