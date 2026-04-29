<img src="https://i.imgur.com/ZG4gSnb.jpeg" alt="demo"/>

# Photography ![OpenCollective](https://opencollective.com/photography/tiers/backer/badge.svg?label=backer&color=brightgreen)
A jekyll website for photographers

## Highlights
1. Easy setup and you get a website of your own for __free__. No web hosting charges too.
2. To add new pictures, you need to just upload them. __No code__ changes required.
3. And, my favorite, you get to see EXIF data like __aperture, shutter speed, iso__ etc. when you click on any image, automagically. Moreover, you can customize this as per your needs.

## Quick Start

**Just follow the below steps and your website would be live in no time:**

1. Fork this repo by hitting the `Fork` button at the top right corner.
2. Deploy to [Netlify](https://netlify.com) — the included `netlify.toml` handles the build automatically. No manual configuration needed.
3. Copy your original photos (straight from your camera) into the `images/` directory and run `gulp resize` locally — this generates the `fulls/` and `thumbs/` folders automatically (see [Image Pipeline](#image-pipeline)).
4. Push `images/fulls/` and `images/thumbs/` to your repo — Netlify will redeploy.
5. Update `_config.yml` with your own details: set `url` to your Netlify domain, and update `title`, `author`, `footer`, and `social_urls`.

And, of course, you don't want someone else's name at the bottom to show up. You can change it in `_config.yml` file as well as a few other settings like your social links, google analytics, etc.

## Run the website locally to test
1. `$ cd photography` - go to the project directory
2. `$ bundle install` - install gems
3. Change the `baseurl` in `_config.yml` to an empty string `""`
4. `$ bundle exec jekyll serve` - start/run the website

### Build the website
1. `$ cd photography` - go to the project directory
2. `$ npm install -g gulp-cli` - install the Gulp CLI globally (one-time setup)
3. `$ npm install` - install all npm dependencies
4. `$ gulp` - minify css, js, resize images, etc.

Note: You only need to build the website if you make changes such as replacing the images, modifying the css styles, etc.

## Image Pipeline

Image processing uses [sharp](https://sharp.pixelplumbing.com/) — a pure Node.js library with no external binary dependencies (no ImageMagick or GraphicsMagick required).

### Output formats and why

| Folder | Format | Size | Reason |
|--------|--------|------|--------|
| `images/fulls/` | AVIF (quality 55) | 2500px wide | AVIF offers ~75% smaller files than JPEG at equivalent visual quality. Used for the lightbox click-through view. |
| `images/thumbs/` | JPEG (quality 85) | 512px wide | Kept as JPEG because the `exif.js` library reads camera metadata (aperture, shutter speed, ISO) directly from the image binary, and it only understands JPEG. Converting thumbs to AVIF would silently break the EXIF caption feature. |

### Filename sanitisation

The pipeline automatically:
- Strips leading underscores (e.g. `_DSC0150.jpg` → `DSC0150`) — Jekyll's static file scanner excludes any file whose name begins with `_`, so they would never appear on the site.
- Replaces spaces and parentheses with underscores (e.g. `DSC1680 (2).jpg` → `DSC1680_2_.jpg`) — spaces in filenames produce unencoded URLs that can break image loading in some browsers.

### How to add or replace images

1. Copy your original photos (JPG, straight from camera) into the `images/` directory _(not into `fulls/` or `thumbs/` — those are generated automatically)_
2. Run `$ gulp resize` — fulls and thumbs are generated and sanitised automatically
3. Push your changes: `$ git add images/ && git commit -m "update photos" && git push`

### Contact Form
You can make the contact form work without the need of any server-side code. Just follow this [article on github](https://github.com/dwyl/html-form-send-email-via-google-script-without-server) which uses a simple google script to send emails or to upload to a google spreadsheet when someone submits the form.

## Credits
Thanks to [AJ](https://twitter.com/ajlkn) for the website template which I enhanced for [jekyll](http://jekyllrb.com/).

## Sponsors

Proudly sponsored by these awesome apps. Support this project by becoming a sponsor. Your logo will show up here with a link to your website. [[Become a sponsor](https://x.com/rampatra_)]

<table>
    <tr>
        <td>
            <a href="https://presentifyapp.com/" target="_blank"><img src="https://raw.githubusercontent.com/rampatra/assets/refs/heads/main/Presentify/Icons/icon_512.png" width="150" height="150"></a>
        </td>
        <td>
            <a href="https://facescreenapp.com/" target="_blank"><img src="https://github.com/user-attachments/assets/b251b413-ccc4-48f1-a316-c2c2a71f959e" width="150" height="150"></a>
        </td>
        <td>
            <a href="https://keyscreenapp.com" target="_blank"><img src="https://github.com/user-attachments/assets/4b75a739-b4b5-432c-a03c-a9bdd8309934" width="150" height="150"></a>
        </td>
        <td>
            <a href="https://todobarapp.com/" target="_blank"><img src="https://todobarapp.com/assets/img/todobar/app-icon-512.png" width="150" height="150"></a>
        </td>
        <td>
            <a href="https://simplefillapp.com/" target="_blank"><img src="https://github.com/user-attachments/assets/6c575d9c-b65b-4ce7-a468-30f74cfedf18" width="150" height="150"></a>
        </td>
    </tr>
</table>

---

_P.S. For any queries or concerns, you can reach out to me on [Twitter](https://twitter.com/rampatra_). I'll try my best to help 🙏._
