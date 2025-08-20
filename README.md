![kagi-earth](/images/kagi-earth-updated.png "Kagi Earth")

# 🌍 Kagi Earth

A lightweight API that serves random satellite imagery from Google Earth for use as dynamic backgrounds in Kagi Search.

## What It Does

Creates a Cloudflare Worker that randomly selects and serves images from Google's Pretty Earth collection. Designed specifically to work with Kagi Search's custom CSS feature to enable Google Earth images as home page backgrounds that change on every page load:

<img src="/images/kagi-earth-screenshot-1.png" width="500"><img src="/images/kagi-earth-screenshot-2.png" width="500"><img src="/images/kagi-earth-screenshot-3.png" width="500"><img src="/images/kagi-earth-screenshot-4.png" width="500">

## Quick Start

### Option 1: One-Click Deploy (Recommended)

1. Click the **Deploy to Cloudflare** button:<br>
[![Deploy to Cloudflare](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https%3A%2F%2Fgithub.com%2Fconnorshinn%2Fkagi-earth)
2. Sign in to your Cloudflare account (or create a free one)
3. Follow the deployment wizard
4. Your API will be available at a URL that looks similar to the following: `https://[your-worker-name].workers.dev/`

### Option 2: Manual Deploy

1. Copy the `worker.js` file from this repository
2. Go to Cloudflare Dashboard → [Workers & Pages](https://dash.cloudflare.com/?to=/:account/workers-and-pages) → Create → Select the ["Start with Hello World" template](https://dash.cloudflare.com/](https://dash.cloudflare.com/?to=/:account/workers-and-pages/static-templates/hello-world)
4. Paste the code from worker.js and click Deploy

## Usage

### In Kagi Search

#### Basic Setup

Add this to your [Kagi Custom CSS](https://kagi.com/settings?p=custom_css):

```css
body:has(div.clouds) {
  background-image: url('https://[your-worker-name].workers.dev/');
  background-size: cover;
  background-position: center;
}
```

The background will be a different random satellite image on each page load!

#### ⚠️ Important: Text Readability

The satellite imagery can make text difficult to read. You'll likely need to add CSS overlays or adjustments for better readability:

```css
/* Example: Add a semi-transparent overlay for better text contrast */
.search-result, .sri-group {
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  padding: 15px;
  border-radius: 8px;
  margin-bottom: 10px;
}
```

#### Complete Theme

This repository includes `custom.css`, a add-on to [pdanzma's excellent Glassmorphism theme](https://github.com/pdanzma/kagi-css) that:
- Ensures text readability with proper overlays and shadows
- Styles homepage elements to work with most image backgrounds

To use kagi-earth with Glassmorphism, simply append the `custom.css` to the end of the Glassmorphism CSS, making sure to replace `[your-worker-URL]` with your Cloudflare Worker URL.

## Technical Details

- **Hosting**: Cloudflare Workers (serverless edge computing)
- **Image Source**: Google Pretty Earth (`gstatic.com`)
- **Performance**: ~50ms response time globally
- **Cost**: Free (100,000 requests/day on Cloudflare's free tier)
- **Caching**: Disabled to ensure random images on each load

## Why Cloudflare Workers?

- **No server needed**: Runs on Cloudflare's edge network
- **Global performance**: Served from 200+ locations worldwide
- **Generous free tier**: 100,000 requests per day
- **Simple deployment**: One JavaScript file, no dependencies

## Troubleshooting

**Images not changing?**
- Clear your browser cache
- The Worker sets `no-cache` headers but some browsers may still cache

**Specific ID not working?**
- Only IDs 1, 2, 3, and 10 are enabled by default
- Edit `ALLOWED_IDS` in the code to add more

**CORS errors?**
- The Worker includes CORS headers
- This shouldn't be an issue with Kagi CSS

## Contributing

Feel free to fork and customize! Some ideas:
- Add more image IDs to the selection pool
- Implement time-based image rotation
- Add weather-based image selection

## License

MIT

## Credits

- Satellite imagery from [Google Earth](https://earth.google.com/)
- Inspired by Pretty Earth's beautiful collection
- Built for the [Kagi Search](https://kagi.com/) community

---

*Enjoy beautiful Earth views with every search! 🌎*


[![Deploy to Cloudflare](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https%3A%2F%2Fgithub.com%2Fconnorshinn%2Fkagi-earth)


# 🌍 Kagi Earth

A lightweight API that serves random satellite imagery from Google Earth for use as dynamic backgrounds in Kagi Search.

[![Deploy to Cloudflare](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https%3A%2F%2Fgithub.com%2Fconnorshinn%2Fkagi-earth)

## What It Does

This Cloudflare Worker randomly selects and serves satellite images from Google's Pretty Earth collection. It's designed specifically to work with Kagi Search's custom CSS feature, providing beautiful Earth imagery as backgrounds that change on every page load.

**Note:** Image backgrounds can impact text readability. This repository includes a complete CSS theme (`kagi-theme.css`) that ensures your Kagi interface remains readable and beautiful.

## Quick Start

### Option 1: One-Click Deploy (Recommended)

1. Click the **Deploy to Cloudflare** button above
2. Sign in to your Cloudflare account (or create a free one)
3. Follow the deployment wizard
4. Your API will be available at: `https://[your-worker-name].workers.dev/`

### Option 2: Manual Deploy

1. Copy the `worker.js` file from this repository
2. Go to [Cloudflare Dashboard](https://dash.cloudflare.com/) → Workers & Pages
3. Create a new Worker
4. Paste the code and deploy

## Usage

### In Kagi Search

#### Basic Setup

Add this to your [Kagi Custom CSS](https://kagi.com/settings?p=custom_css):

```css
body {
  background-image: url('https://[your-worker-name].workers.dev/');
  background-size: cover;
  background-position: center;
  background-attachment: fixed;
}
```

The background will be a different random satellite image on each page load!

#### ⚠️ Important: Text Readability

The satellite imagery can make text difficult to read. You'll likely need to add CSS overlays or adjustments for better readability:

```css
/* Example: Add a semi-transparent overlay for better text contrast */
.search-result, .sri-group {
  background: rgba(255, 255, 255, 0.95);
  backdrop-filter: blur(10px);
  padding: 15px;
  border-radius: 8px;
  margin-bottom: 10px;
}
```

#### Complete Theme

This repository includes `kagi-theme.css`, a comprehensive CSS theme based on [pdanzma's beautiful Kagi CSS theme](https://github.com/pdanzma/kagi-css) that:
- Ensures text readability with proper overlays and shadows
- Styles all Kagi UI elements to work with image backgrounds
- Includes hover effects and smooth transitions
- Maintains accessibility while adding visual appeal

To use the complete theme, copy the contents of `kagi-theme.css` and replace `[your-worker-name]` with your Cloudflare Worker URL.

### API Endpoints

| Endpoint | Description | Example |
|----------|-------------|---------|
| `/` | Returns a random image | `https://your-worker.workers.dev/` |
| `/?id=3` | Returns a specific image by ID | `https://your-worker.workers.dev/?id=3` |
| `/?metadata=true` | Returns JSON metadata instead of image | `https://your-worker.workers.dev/?metadata=true` |

### Available Image IDs

This instance is configured to serve a curated selection of images:
- **ID 1**: Satellite view 1
- **ID 2**: Satellite view 2  
- **ID 3**: Satellite view 3
- **ID 10**: Satellite view 10

## How It Works

1. **Request**: When you load a Kagi page, your CSS requests an image from the Worker
2. **Selection**: The Worker randomly picks one of the available image IDs
3. **Redirect**: The Worker redirects to the image hosted on Google's servers (`gstatic.com`)
4. **Display**: The image loads as your background (Kagi's security policy allows `gstatic.com`)

## Configuration

To modify the available images, edit the `ALLOWED_IDS` array in `worker.js`:

```javascript
const ALLOWED_IDS = [1, 2, 3, 10]; // Change these to any valid Pretty Earth IDs (1-7023)
```

## Technical Details

- **Hosting**: Cloudflare Workers (serverless edge computing)
- **Image Source**: Google Pretty Earth (`gstatic.com`)
- **Performance**: ~50ms response time globally
- **Cost**: Free (100,000 requests/day on Cloudflare's free tier)
- **Caching**: Disabled to ensure random images on each load

## Why Cloudflare Workers?

- **No server needed**: Runs on Cloudflare's edge network
- **Global performance**: Served from 200+ locations worldwide
- **Generous free tier**: 100,000 requests per day
- **Simple deployment**: One JavaScript file, no dependencies

## Troubleshooting

**Images not changing?**
- Clear your browser cache
- The Worker sets `no-cache` headers but some browsers may still cache

**Specific ID not working?**
- Only IDs 1, 2, 3, and 10 are enabled by default
- Edit `ALLOWED_IDS` in the code to add more

**CORS errors?**
- The Worker includes CORS headers
- This shouldn't be an issue with Kagi CSS

## Contributing

Feel free to fork and customize! Some ideas:
- Add more image IDs to the selection pool
- Implement time-based image rotation
- Add weather-based image selection

## License

MIT

## Credits

- Satellite imagery from [Google Earth](https://earth.google.com/)
- CSS theme based on [pdanzma's Kagi CSS](https://github.com/pdanzma/kagi-css)
- Inspired by Pretty Earth's beautiful collection
- Built for the [Kagi Search](https://kagi.com/) community

---

*Enjoy beautiful Earth views with every search! 🌎*
