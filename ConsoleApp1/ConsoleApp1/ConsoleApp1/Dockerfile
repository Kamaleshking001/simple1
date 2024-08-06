# Use the official .NET SDK image as a build environment
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build

# Set the working directory inside the container
WORKDIR /app

# Copy the project file and restore dependencies
COPY *.csproj ./
RUN dotnet restore

# Copy the rest of the application code
COPY . ./

# Build the application
RUN dotnet publish -c Release -o out

# Use the official .NET Runtime image as the runtime environment
FROM mcr.microsoft.com/dotnet/runtime:7.0

# Set the working directory inside the container
WORKDIR /app

# Copy the compiled application from the build image
COPY --from=build /app/out .

# Specify the command to run the application
ENTRYPOINT ["dotnet", "ConsoleApp1.dll"]
