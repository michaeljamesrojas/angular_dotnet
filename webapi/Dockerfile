# Use the official .NET Core SDK image as the base
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build

# Set the working directory in the container
WORKDIR /app

# Copy the .NET project file and restore dependencies
COPY *.csproj ./
RUN dotnet restore

# Copy the entire project and build the application
COPY . ./
RUN dotnet publish -c Release -o out

# Use the official ASP.NET Core runtime image as the base
FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS runtime

# Set the working directory in the container
WORKDIR /app

# Copy the published application from the build stage
COPY --from=build /app/out ./

# Expose the port your application listens on
EXPOSE 80

# Set the entry point for the container
ENTRYPOINT ["dotnet", "webapi.dll"]