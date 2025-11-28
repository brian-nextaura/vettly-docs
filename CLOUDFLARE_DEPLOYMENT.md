# Vettly Docs - Cloudflare Pages Deployment Guide

This guide covers deploying the Vettly documentation site to Cloudflare Pages.

## Overview

The Vettly documentation site is built with VitePress and generates a static site perfect for Cloudflare Pages deployment.

- **Framework**: VitePress 1.6.x
- **Build Output**: `docs/.vitepress/dist`
- **Build Time**: ~9 seconds
- **Deployment**: Static HTML + assets

## Prerequisites

1. **Cloudflare Account**: Sign up at [cloudflare.com](https://cloudflare.com)
2. **GitHub Repository**: Fork or have access to [brian-nextaura/vettly-docs](https://github.com/brian-nextaura/vettly-docs)
3. **Domain**: A domain managed in Cloudflare (e.g., `vettly.com`)

## Deployment Steps

### Option 1: Cloudflare Dashboard (Recommended)

1. **Connect Repository**
   - Go to Cloudflare Dashboard → Pages
   - Click "Create a project"
   - Connect your GitHub account
   - Select the `vettly-docs` repository

2. **Configure Build Settings**
   ```
   Framework preset: None (or VitePress if available)
   Build command: bun run build
   Build output directory: docs/.vitepress/dist
   Root directory: /
   ```

3. **Environment Variables** (if needed)
   - Currently no environment variables required
   - The docs are public and don't need secrets

4. **Advanced Settings**
   - Node version: 18 or higher
   - Build timeout: Default (10 minutes) is fine
   - Build watch paths: Leave default

5. **Deploy**
   - Click "Save and Deploy"
   - Wait ~2 minutes for first build
   - Your docs will be available at `[project-name].pages.dev`

### Option 2: Wrangler CLI

1. **Install Wrangler**
   ```bash
   bun add -g wrangler
   ```

2. **Login to Cloudflare**
   ```bash
   wrangler login
   ```

3. **Build the Docs**
   ```bash
   cd /path/to/vettly-docs
   bun run build
   ```

4. **Deploy**
   ```bash
   wrangler pages deploy docs/.vitepress/dist --project-name=vettly-docs
   ```

## Custom Domain Setup

### Configure docs.vettly.com

1. **In Cloudflare Pages**:
   - Go to your Pages project → Custom domains
   - Click "Set up a custom domain"
   - Enter `docs.vettly.com`

2. **DNS Configuration**:
   - Cloudflare will automatically create a CNAME record
   - If you need to do it manually:
     ```
     Type: CNAME
     Name: docs
     Target: [your-project].pages.dev
     Proxy: Enabled (orange cloud)
     ```

3. **SSL/TLS**:
   - Automatically provisioned by Cloudflare
   - Usually takes 1-5 minutes
   - Use "Full" SSL/TLS encryption mode

## Continuous Deployment

### Automatic Deployments

Cloudflare Pages automatically deploys when you push to GitHub:

- **Production Branch**: `main` → deploys to `docs.vettly.com`
- **Preview Branches**: All other branches → preview URLs

### Branch Configuration

1. **Production branch**: `main`
2. **Preview deployments**: Enabled for all branches
3. **Build settings**: Same for all branches

## Build Configuration

### package.json Scripts

```json
{
  "scripts": {
    "dev": "bun run --filter './packages/*' build && bun run --filter './docs' dev",
    "build": "bun run build:packages && bun run build:docs",
    "build:packages": "bun run --filter './packages/*' build",
    "build:docs": "bun run --filter './docs' build",
    "preview": "bun run --filter './docs' preview"
  }
}
```

### Build Process

1. Builds workspace packages (`@nextauralabs/vettly-sdk`, `@nextauralabs/vettly-react`)
2. Builds VitePress documentation site
3. Output: Static HTML in `docs/.vitepress/dist`

## Performance Optimization

### Cloudflare Edge Features

1. **Enable Features**:
   - Auto Minify: HTML, CSS, JS
   - Brotli compression
   - HTTP/3 (QUIC)
   - 0-RTT Connection Resumption

2. **Caching**:
   - Static assets cached at edge
   - Versioned assets have long cache times
   - HTML pages: short cache with revalidation

### VitePress Optimization

Already configured in the docs:
- Code splitting
- CSS extraction
- Asset optimization
- Search indexing

## Monitoring

### Cloudflare Analytics

Access analytics in Cloudflare Pages dashboard:
- Page views
- Unique visitors
- Bandwidth usage
- Response times
- Geographic distribution

### Build Status

Monitor deployments:
- Build logs available in dashboard
- Webhook notifications (optional)
- Email alerts for failed builds

## Troubleshooting

### Build Fails

**Check Node Version**:
```bash
# Ensure using Node 18+
node --version
```

**Clear Build Cache**:
- In Cloudflare Pages, go to Settings → Builds → Clear cache
- Retry deployment

**Workspace Dependencies**:
- Ensure all workspace packages build successfully
- Check `packages/vettly-sdk` and `packages/vettly-react`

### Deployment Issues

**404 on Pages**:
- Verify build output directory is `docs/.vitepress/dist`
- Check that `index.html` exists in output

**CSS/JS Not Loading**:
- Check VitePress base URL configuration
- Ensure all assets are in the dist folder

**Search Not Working**:
- VitePress local search is client-side (no config needed)
- Ensure search index is generated during build

## VitePress Configuration

### Current Config Location

`docs/.vitepress/config.ts` contains:
- Site metadata
- Navigation structure
- Theme configuration
- Plugin settings

### Base URL (Important!)

For custom domain, ensure `config.ts` has:
```typescript
export default defineConfig({
  // For docs.vettly.com
  base: '/',

  // Other config...
})
```

## Integration with Main Site

### Link from Main Website

The main Vettly website should link to docs:

```tsx
// In website navbar
<Link href="https://docs.vettly.com">Documentation</Link>
```

### Consistent Branding

Ensure docs match main site:
- Same color scheme (emerald primary)
- Consistent dark theme
- Same logo and branding

## Security

### Headers

Configure security headers in Cloudflare Pages:
```
X-Frame-Options: SAMEORIGIN
X-Content-Type-Options: nosniff
Referrer-Policy: strict-origin-when-cross-origin
```

### Access Control

Docs are public by default. For private docs:
- Use Cloudflare Access
- Configure authentication rules
- Requires Cloudflare Teams subscription

## Cost

Cloudflare Pages is **free** for:
- Unlimited requests
- Unlimited bandwidth
- Unlimited builds
- 500 builds/month
- 20,000 files per deployment

Perfect for documentation sites!

## Post-Deployment Checklist

- [ ] Docs site accessible at `docs.vettly.com`
- [ ] SSL certificate active
- [ ] Navigation works correctly
- [ ] Search functionality operational
- [ ] Code examples render properly
- [ ] All links working (no 404s)
- [ ] Mobile responsive
- [ ] Lighthouse score > 95
- [ ] Analytics tracking enabled
- [ ] Main website links to docs

## Updating Documentation

1. **Edit Markdown Files**:
   ```bash
   cd /path/to/vettly-docs/docs
   # Edit .md files in docs/guide/, docs/api/, etc.
   ```

2. **Test Locally**:
   ```bash
   bun run dev
   # Visit http://localhost:5173
   ```

3. **Commit and Push**:
   ```bash
   git add .
   git commit -m "Update documentation"
   git push origin main
   ```

4. **Automatic Deployment**:
   - Cloudflare detects push
   - Builds and deploys automatically
   - Available at docs.vettly.com in ~2 minutes

## Support Links

- VitePress Docs: https://vitepress.dev
- Cloudflare Pages Docs: https://developers.cloudflare.com/pages/
- Cloudflare Dashboard: https://dash.cloudflare.com/

## Need Help?

- VitePress Discord: https://discord.gg/vitepress
- Cloudflare Community: https://community.cloudflare.com/
- GitHub Issues: https://github.com/brian-nextaura/vettly-docs/issues
