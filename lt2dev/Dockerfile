# Stage 1: Build
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copy project file và restore (cache tốt)
COPY *.csproj ./
RUN dotnet restore

# Copy toàn bộ source code
COPY . ./

# Publish ra thư mục /app/publish
RUN dotnet publish -c Release -o /app/publish

# Stage 2: Runtime
FROM mcr.microsoft.com/dotnet/aspnet:8.0
WORKDIR /app

# Set URL để ASP.NET Core listen trên mọi interface
ENV ASPNETCORE_URLS=http://+:80

# Copy output từ stage build
COPY --from=build /app/publish .

# Expose port
EXPOSE 80

# Chạy app
ENTRYPOINT ["dotnet", "lt2dev.dll"]
