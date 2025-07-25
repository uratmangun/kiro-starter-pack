# 🌐 Cloudflare Pages Deployment Setup

This guide will help you set up automatic deployment to Cloudflare Pages with GitHub Actions.

## 📋 Prerequisites

1. **Cloudflare Account** - Sign up at [cloudflare.com](https://cloudflare.com)
2. **GitHub Repository** - Your repository with the index.html file
3. **Cloudflare Pages Project** - Create a new Pages project

## 🔧 Setup Steps

### 1. Create Cloudflare Pages Project

1. Go to [Cloudflare Dashboard](https://dash.cloudflare.com)
2. Navigate to **Pages** in the sidebar
3. Click **Create a project**
4. Choose **Direct Upload** (not Git integration)
5. Name your project (e.g., `kiro-starter-pack`)
6. Note down your **Account ID** and **Project Name**

### 2. Get Cloudflare API Token

1. Go to [Cloudflare API Tokens](https://dash.cloudflare.com/profile/api-tokens)
2. Click **Create Token**
3. Use the **Custom token** template
4. Configure the token with these permissions:
   - **Account** - `Cloudflare Pages:Edit`
   - **Zone** - `Zone:Read` (if using custom domain)
   - **Account Resources** - Include `All accounts` or your specific account
5. Copy the generated token

### 3. Configure GitHub Secrets

Go to your GitHub repository settings and add these secrets:

#### Required Secrets:
- `CLOUDFLARE_API_TOKEN` - Your Cloudflare API token from step 2
- `CLOUDFLARE_ACCOUNT_ID` - Your Cloudflare Account ID

#### Required Variables:
- `CLOUDFLARE_PROJECT_NAME` - Your Cloudflare Pages project name

### 4. Add Secrets to GitHub

1. Go to your repository on GitHub
2. Click **Settings** → **Secrets and variables** → **Actions**
3. Click **New repository secret** and add:

```
Name: CLOUDFLARE_API_TOKEN
Value: [Your Cloudflare API Token]
```

```
Name: CLOUDFLARE_ACCOUNT_ID  
Value: [Your Cloudflare Account ID]
```

4. Click **Variables** tab and add:

```
Name: CLOUDFLARE_PROJECT_NAME
Value: [Your Cloudflare Pages Project Name]
```

## 🚀 How It Works

The GitHub Action will:

1. **Trigger** on pushes to main/master branch when `index.html` changes
2. **Deploy** the site to Cloudflare Pages
3. **Update** the GitHub repository homepage URL automatically
4. **Comment** on PRs with deployment preview links
5. **Create** deployment status for tracking

## 🔍 Finding Your Cloudflare Account ID

1. Go to [Cloudflare Dashboard](https://dash.cloudflare.com)
2. Select any domain or go to the right sidebar
3. Your Account ID is displayed in the right sidebar under **API**

## 🌐 Custom Domain (Optional)

To use a custom domain:

1. In Cloudflare Pages, go to your project
2. Click **Custom domains** tab
3. Add your domain and follow DNS setup instructions
4. The GitHub Action will automatically use your custom domain URL

## 🔧 Troubleshooting

### Common Issues:

1. **Invalid API Token**
   - Ensure token has correct permissions
   - Check token hasn't expired

2. **Wrong Account ID**
   - Verify Account ID from Cloudflare dashboard
   - Ensure it matches the account where Pages project exists

3. **Project Not Found**
   - Verify project name matches exactly
   - Ensure project exists in Cloudflare Pages

### Debug Steps:

1. Check GitHub Actions logs for detailed error messages
2. Verify all secrets and variables are set correctly
3. Test API token with Cloudflare API directly

## 📝 Manual Deployment

You can also trigger deployment manually:

1. Go to **Actions** tab in your GitHub repository
2. Select **Deploy to Cloudflare Pages and Update Homepage**
3. Click **Run workflow**
4. Choose your branch and click **Run workflow**

## 🎉 Success!

Once configured, every push to your main branch will automatically:
- Deploy your site to Cloudflare Pages
- Update your GitHub repository homepage URL
- Provide fast global CDN delivery
- Enable automatic HTTPS

Your site will be available at: `https://[project-name].pages.dev`
