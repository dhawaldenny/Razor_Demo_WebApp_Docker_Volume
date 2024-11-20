# Razor Project File Change in Docker

This README outlines reflecting changes in Razor files within a Docker environment, where changes to Razor files are instantly reflected in the live environment.

## Problem Overview

### Razor Files:
- When changes are made to Razor files (e.g., `.cshtml`), they are immediately reflected in the live environment when using Docker, as expected.


## Steps to Reproduce Changes in Razor Project (Using Docker)

### 1. Create a New ASP.NET Core MVC Project

1. Create a new ASP.NET Core Web App (MVC) project.
2. In the `Program.cs` file, add the following:

```csharp
builder.Services.AddRazorPages();
builder.Services.AddRazorPages().AddRazorRuntimeCompilation();
app.UseStaticFiles();
```

### 2. Add Docker File

1. Add a Dockerfile to the project.
2. In the Dockerfile, include the following key-value pair to enable file change detection:

```dockerfile
ENV DOTNET_USE_POLLING_FILE_WATCHER=1
```

### 3. Build the Docker Image

Use the following command to build the Docker image:

```bash
docker build -t your_image_name .
```

### 4. Run Docker Container with Volume

When running the Docker container, add a volume to mount the local views directory to the container, allowing changes to be reflected in the live environment:

```bash
docker run -p 5050:80 -v "dynamic_volume_path:/app/Views/:rw" your_image_name
```

### 5. Reproduce Changes in Razor Project

1. Navigate to any `.cshtml` file in the project.
2. Make text changes in the `.cshtml` file.
3. Open your browser and navigate to the appropriate port (e.g., `http://localhost:5050`).
4. The changes should take effect immediately.


