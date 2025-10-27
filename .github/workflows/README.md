# CI/CD Workflow Documentation

## Overview

This repository includes a GitHub Actions workflow that automatically builds the Magnus Chess application and creates releases.

## Features

- **Automated Building**: Compiles the VB.NET Windows Forms application using MSBuild
- **Release Creation**: Packages the executable and creates GitHub Releases
- **Manual Triggering**: Can be triggered manually via workflow_dispatch
- **Tag-based Releases**: Automatically triggers on version tags

## Usage

### Method 1: Manual Trigger (Workflow Dispatch)

1. Navigate to the **Actions** tab in the GitHub repository
2. Select the **Build and Release** workflow from the left sidebar
3. Click the **Run workflow** button
4. Enter a release tag (e.g., `v1.0.0`, `v1.1.0`)
5. Click **Run workflow** to start the build

### Method 2: Automated Trigger (Push Tag)

1. Create and push a version tag:
   ```bash
   git tag v1.0.0
   git push origin v1.0.0
   ```

2. The workflow will automatically:
   - Build the application in Release configuration
   - Package the executable with dependencies
   - Create a GitHub Release with the tag name

## Workflow Steps

1. **Checkout code**: Retrieves the repository code
2. **Setup MSBuild**: Configures MSBuild for .NET Framework projects
3. **Setup NuGet**: Prepares NuGet package manager
4. **Restore packages**: Restores any NuGet dependencies
5. **Build solution**: Compiles the project in Release mode
6. **Create package**: Packages the executable, config, and documentation
7. **Determine tag**: Gets the release tag from trigger
8. **Create release**: Publishes the release to GitHub with the packaged files

## Release Contents

Each release includes:
- `Magnus-Release.zip` containing:
  - `Magnus.exe` - The compiled chess game executable
  - `Magnus.exe.config` - Application configuration file (if present)
  - `LICENSE` - License information
  - `README.md` - Project documentation

## Requirements

The built application requires:
- Windows operating system
- .NET Framework 4.7.2 or higher

## Troubleshooting

If the workflow fails:
1. Check the Actions tab for error logs
2. Ensure the tag format matches `v*` pattern (e.g., `v1.0.0`)
3. Verify that the repository has necessary permissions for creating releases
4. Check that the build configuration is correct in the `.vbproj` file
