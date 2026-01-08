FROM mcr.microsoft.com/dotnet/sdk:10.0-preview AS build
WORKDIR /src

# Copy csproj and restore dependencies
COPY ["Arduino dashboard.csproj", "./"]
RUN dotnet restore "Arduino dashboard.csproj"

# Copy everything else and build
COPY . .
RUN dotnet publish "Arduino dashboard.csproj" -c Release -o /app/publish

# Runtime stage
FROM mcr.microsoft.com/dotnet/aspnet:10.0-preview AS runtime
WORKDIR /app
EXPOSE 13000

COPY --from=build /app/publish .

ENV ASPNETCORE_URLS=http://+:13000
ENV ASPNETCORE_ENVIRONMENT=Production

ENTRYPOINT ["dotnet", "Arduino dashboard.dll"]
