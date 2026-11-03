# WordPress Headless About Page (Vanilla JS)

A simple example of using WordPress as a headless CMS with **plain HTML and
JavaScript**. You don't need a framework, a build step or any dependencies. The
page loads content from the **WordPress REST API** (including **ACF** fields)
and shows it in the browser.

It's a good starting point if you want to learn how headless WordPress works
before you move to a framework like Next.js.

## Features

- **No dependencies.** One `index.html` file using the native `fetch` API.
- **WordPress REST API.** Loads a single page by ID.
- **ACF support.** Shows text, image, group and repeater fields.
- **Loading and error states.** Shows a loader while fetching and a friendly
  message if the request fails.

## Quick Start

1. **Clone the repository**

   ```bash
   git clone https://github.com/yourusername/your-repo-name.git
   cd your-repo-name
   ```

2. **Point it at your WordPress site**

   In `index.html`, change the API URL to your own domain and page ID:

   ```javascript
   fetch("https://your-wordpress-site.com/wp-json/wp/v2/pages/316")
   ```

3. **Open it in a browser**

   You can open `index.html` directly. For the best results, serve it locally:

   ```bash
   npx serve .
   ```

## How It Works

1. The page shows a **Loading...** message.
2. It sends a request to `/wp-json/wp/v2/pages/<id>`.
3. It reads the page title and the ACF fields from the response.
4. It fills the HTML elements with that content, then hides the loader.
5. If anything goes wrong, it shows an error message instead.

## WordPress Setup

### Required plugins

- [Advanced Custom Fields (ACF)](https://wordpress.org/plugins/advanced-custom-fields/)
  — turn on **Show in REST API** in each field group's settings (ACF 6+).

### Expected ACF fields

The script expects these fields on the page. Rename them in `index.html` to
match your own setup.

| Field name | Type | Used for |
| --- | --- | --- |
| `main_heading` | Text | Main heading |
| `description` | Text / WYSIWYG | Intro text |
| `banner_image_url` | Text / URL | Banner image source |
| `our_mission_and_vission_section` | Group | Mission section |
| ↳ `our_mission_heading` | Text | Mission heading |
| ↳ `our_mission_descriptions` | Repeater | Mission paragraphs |
| ↳↳ `our_mission_paragraph` | Text | Single paragraph |
| `accordion_section` | Group | Accordion section |
| ↳ `accordion_main_heading` | Text | Accordion heading |
| ↳ `accordion` | Repeater | Accordion items |
| ↳↳ `heading` | Text | Item heading |
| ↳↳ `description` | Text | Item content |

> **Tip:** ACF image fields return an image ID by default. Set the field's
> return format to **Image URL**, or use a plain URL field as shown above.

### CORS

If the page is hosted on a different domain from WordPress, the browser may
block the request. Allow your frontend's domain on the WordPress side, either
with a CORS plugin or by adding headers in `functions.php`.

## Project Structure

```
├── index.html   # Markup, styles and the fetch script
└── README.md
```

## Good to Know

- Content is added with `innerHTML`, so only use this with a WordPress site
  you trust.
- Search engines may not see content that loads in the browser. If SEO matters,
  use a framework with server-side or static rendering, such as my
  [Next.js WordPress boilerplate](https://github.com/yourusername/nextjs-wp-boilerplate).

## Contributing

Contributions are welcome. Feel free to open an issue or a pull request.

## License

Released under the [MIT License](LICENSE).

---

## Author

Built and maintained by [Hasnat Ahmad](https://www.devhasnatahmad.com/). Need help with a project? [Get in touch](https://www.devhasnatahmad.com/).

If this project saved you time, please give it a ⭐ on GitHub.
