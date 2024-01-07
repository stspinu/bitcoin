FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build-env
WORKDIR /app0

# Copy everything
COPY . ./
# Restore as distinct layers
RUN dotnet restore
# Build and publish a release
RUN dotnet publish -c Release -o out

# Build runtime image
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app0
EXPOSE 80
COPY --from=build-env /app0/out .
ENTRYPOINT ["dotnet", "app0.dll", "--urls", "http://0.0.0.0:80"]
