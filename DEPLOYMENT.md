# Deployment Guide

This guide helps you deploy the Improved Engine website to different hosting platforms.

## GitHub Pages Deployment

GitHub Pages deployment is **already configured** and will happen automatically.

### Setup Steps

1. Go to your repository settings: `https://github.com/Shanshan-Qu/Improved-engine/settings/pages`
2. Under "Build and deployment" → "Source", select **"GitHub Actions"**
3. Push your changes to the `main` branch
4. The workflow will automatically build and deploy your site
5. Your site will be available at: `https://shanshan-qu.github.io/Improved-engine/`

### Manual Deployment

You can also manually trigger the deployment:
1. Go to the "Actions" tab in your repository
2. Select "Deploy MkDocs to GitHub Pages"
3. Click "Run workflow"

## Azure Static Web Apps Deployment

Follow these steps to deploy to Azure Static Web Apps:

### Prerequisites

- An Azure account ([Sign up for free](https://azure.microsoft.com/free/))
- Azure CLI installed (optional, for command-line deployment)

### Option 1: Deploy via Azure Portal (Recommended)

1. **Create a Static Web App**
   - Go to [Azure Portal](https://portal.azure.com)
   - Click "Create a resource" → Search for "Static Web App"
   - Click "Create"

2. **Configure Basic Settings**
   - **Subscription**: Select your subscription
   - **Resource Group**: Create new or select existing
   - **Name**: `improved-engine` (or your preferred name)
   - **Plan type**: Free (for testing) or Standard (for production)
   - **Region**: Choose closest to your users
   - **Deployment source**: GitHub

3. **Connect to GitHub**
   - Click "Sign in with GitHub"
   - Authorize Azure Static Web Apps
   - Select:
     - **Organization**: Shanshan-Qu
     - **Repository**: Improved-engine
     - **Branch**: main

4. **Configure Build Details**
   - **Build Presets**: Custom
   - **App location**: `/`
   - **Api location**: (leave empty)
   - **Output location**: `site`

5. **Add Build Configuration**
   - Under "Build" tab, add this command:
     ```
     pip install -r requirements.txt && mkdocs build
     ```

6. **Review and Create**
   - Click "Review + create"
   - Click "Create"
   - Azure will create a workflow file in your repository

7. **Wait for Deployment**
   - Go to the "Actions" tab in GitHub
   - Wait for the Azure Static Web Apps deployment to complete
   - Your site URL will be shown in the Azure portal

### Option 2: Deploy via Azure CLI

```bash
# Login to Azure
az login

# Create a resource group
az group create --name improved-engine-rg --location "East US"

# Create a static web app
az staticwebapp create \
  --name improved-engine \
  --resource-group improved-engine-rg \
  --source https://github.com/Shanshan-Qu/Improved-engine \
  --location "East US" \
  --branch main \
  --app-location "/" \
  --output-location "site" \
  --login-with-github
```

### Option 3: Use the Provided Workflow File

A workflow file for Azure Static Web Apps has been created at `.github/workflows/azure-static-web-apps.yml` (if you choose to add it). The workflow includes:

```yaml
name: Azure Static Web Apps CI/CD

on:
  push:
    branches:
      - main
  pull_request:
    types: [opened, synchronize, reopened, closed]
    branches:
      - main

jobs:
  build_and_deploy_job:
    runs-on: ubuntu-latest
    name: Build and Deploy Job
    steps:
      - uses: actions/checkout@v3
        with:
          submodules: true
      
      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.x'
      
      - name: Install dependencies
        run: pip install -r requirements.txt
      
      - name: Build site
        run: mkdocs build
      
      - name: Deploy to Azure Static Web Apps
        uses: Azure/static-web-apps-deploy@v1
        with:
          azure_static_web_apps_api_token: ${{ secrets.AZURE_STATIC_WEB_APPS_API_TOKEN }}
          repo_token: ${{ secrets.GITHUB_TOKEN }}
          action: "upload"
          app_location: "site"
          skip_app_build: true
```

## Custom Domain Setup

### For GitHub Pages

1. Go to repository Settings → Pages
2. Under "Custom domain", enter your domain (e.g., `www.improved-engine.com`)
3. Create a CNAME record in your DNS settings pointing to `shanshan-qu.github.io`
4. Wait for DNS propagation (can take up to 24 hours)
5. Enable "Enforce HTTPS"

### For Azure Static Web Apps

1. Go to your Static Web App in Azure Portal
2. Click "Custom domains" in the left menu
3. Click "Add"
4. Enter your domain name
5. Follow the instructions to add DNS records
6. Wait for validation
7. Azure automatically provides free SSL certificates

## Environment-Specific Configuration

### Update Site URL

Edit `mkdocs.yml` and update the `site_url` for your deployment:

```yaml
# For GitHub Pages
site_url: https://shanshan-qu.github.io/Improved-engine/

# For Azure Static Web Apps with custom domain
site_url: https://your-domain.com/

# For Azure Static Web Apps default domain
site_url: https://your-app-name.azurestaticapps.net/
```

## Troubleshooting

### Build Fails on Azure

- Ensure Python 3.x is specified in the build command
- Check that `requirements.txt` is in the root directory
- Verify the output location is set to `site`

### Site Doesn't Load Correctly

- Check that the `site_url` in `mkdocs.yml` matches your deployment URL
- Clear your browser cache
- Check browser console for errors

### GitHub Actions Fails

- Ensure GitHub Pages is enabled in repository settings
- Check that the workflow has appropriate permissions
- Review the workflow logs for specific errors

### Contact Form Not Working

- The contact form needs to be configured with a form service
- See instructions in `docs/contact.md`
- Recommended services: Formspree, Netlify Forms, or custom backend

## Monitoring and Analytics

### Add Google Analytics (Optional)

Edit `mkdocs.yml` and add:

```yaml
extra:
  analytics:
    provider: google
    property: G-XXXXXXXXXX
```

### Azure Application Insights (Optional)

For Azure deployments, you can enable Application Insights for monitoring:

1. Create an Application Insights resource
2. Get the connection string
3. Add it to your Azure Static Web App configuration

## Next Steps

1. Enable GitHub Pages following the steps above
2. Test the deployment
3. Set up custom domain (if desired)
4. Configure the contact form
5. Add your own content and blog posts
6. Monitor the site performance

For more help, see:
- [MkDocs Documentation](https://www.mkdocs.org/)
- [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)
- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [Azure Static Web Apps Documentation](https://docs.microsoft.com/en-us/azure/static-web-apps/)
