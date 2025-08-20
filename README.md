![kagi-earth](/images/kagi-earth-updated.png "Kagi Earth")

# 🌍 Kagi Earth

A lightweight API that serves random satellite imagery from Google Earth for use as dynamic backgrounds in Kagi Search.

## What It Does

Creates a Cloudflare Worker that randomly selects and serves images from Google's Pretty Earth collection. Designed specifically to work with Kagi Search's custom CSS feature to enable Google Earth images as home page backgrounds that change on every page load:

<img align="center" src="/images/kagi-earth-screenshot-1.png" width="410"><img align="center" src="/images/kagi-earth-screenshot-2.png" width="410"><img align="center" src="/images/kagi-earth-screenshot-3.png" width="410"><img align="center" src="/images/kagi-earth-screenshot-4.png" width="410">

## Quick Start

### Option 1: One-Click Deploy (Recommended)

1. Click the **Deploy to Cloudflare** button:<br>
[![Deploy to Cloudflare](https://deploy.workers.cloudflare.com/button)](https://deploy.workers.cloudflare.com/?url=https%3A%2F%2Fgithub.com%2Fconnorshinn%2Fkagi-earth)
2. Sign in to your Cloudflare account (or create a free one)
3. Follow the deployment wizard
4. Your API will be available at a URL that looks similar to the following: `https://[your-worker-name].workers.dev/`

> [!TIP]
> App can be deployed via Cloudflare's free tier, which provides 100,000 requests/day at no cost

### Option 2: Manual Deploy

1. Copy the `worker.js` file from this repository
2. Go to Cloudflare Dashboard → [Workers & Pages](https://dash.cloudflare.com/?to=/:account/workers-and-pages) → Create → Select the ["Start with Hello World" template](https://dash.cloudflare.com/](https://dash.cloudflare.com/?to=/:account/workers-and-pages/static-templates/hello-world)
4. Paste the code from worker.js and click Deploy

## Usage

### In Kagi Search

#### Basic Setup

Add this to your [Kagi Custom CSS](https://kagi.com/settings?p=custom_css):

```css
body:has(.clouds) {
  background-image: url('https://[your-worker-name].workers.dev/');
  background-size: cover;
  background-position: center;
}
```

The background will be a different random satellite image on each page load!

#### ⚠️ Important: Text Readability

The satellite imagery can make some of the text elements on the home page difficult to read. You'll likely need to add CSS overlays or adjustments for better readability. See additional Complete Theme section below for more details. 

```css
/* Example: Add a semi-transparent overlay for better text contrast */
body:has(.clouds) {
  background-image: url("https://kagi-earth.connor-shinn.workers.dev");
  background-size: cover;
  background-position: center;

  .landing-category-select._0_land_cat_box {
    background-color: rgba(0, 0, 0, 0.3);
    -webkit-backdrop-filter: blur(5px);
    backdrop-filter: blur(5px);
    padding: 20px;
    margin: 30px 30px 30px 0px;
    border-radius: 10px;
    padding: 0px 10px 15px 10px;
  }
}
```

#### Complete Theme

This repository includes `custom.css`, an add-on to [pdanzma's excellent Glassmorphism theme](https://github.com/pdanzma/kagi-css) that:
- Ensures text readability with proper overlays and shadows
- Styles homepage elements to work with most Google Earth backgrounds

To use kagi-earth with Glassmorphism, simply append the `custom.css` to the end of the Glassmorphism CSS, making sure to replace `[your-worker-URL]` with your Cloudflare Worker URL.

##Contributing
This is still very much a work in progress, so please feel free to open an issue or pull request if you encounter any bugs or would like to contribute. 

Credits
Created by pdanzma. Inspired by modern search UIs (e.g., Google and Brave) with many original touches.

## Credits

- Inspired by satellite imagery from [Google Earth](https://earth.google.com/) and the Pretty Earth collection
- Custom CSS file based on [pdanzma's Glassmorphism theme](https://github.com/pdanzma/kagi-css)
- Built for the [Kagi Search](https://kagi.com/) community

---

*Enjoy beautiful Earth views with every search! 🌎*
