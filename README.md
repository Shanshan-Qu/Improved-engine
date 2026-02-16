# Improved Engine

A modern, responsive website built with MkDocs Material theme, featuring a gradient color scheme, light/dark mode support, and full accessibility.

## Features

- ✨ **Responsive Design** - Works seamlessly on desktop, tablet, and mobile devices
- 🌓 **Light/Dark Mode** - Automatic theme switching based on user preference
- ♿ **Accessible** - Built with WCAG guidelines in mind
- 🎨 **Gradient Theme** - Beautiful purple gradient color scheme
- 🖼️ **Hero Images** - Eye-catching hero sections on every page
- 📝 **Blog System** - Easy-to-manage blog with post categorization
- 📧 **Contact Page** - Ready-to-use contact form
- 🚀 **Fast Performance** - Optimized for speed and SEO

## Quick Start

### Prerequisites

- Python 3.x
- pip (Python package manager)

### Installation

1. Clone the repository:
```bash
git clone https://github.com/Shanshan-Qu/Improved-engine.git
cd Improved-engine
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Run the development server:
```bash
mkdocs serve
```

4. Open your browser and visit: `http://127.0.0.1:8000`

## Building the Site

To build the static site:

```bash
mkdocs build
```

The built site will be in the `site/` directory.

## Deployment

### GitHub Pages

The site automatically deploys to GitHub Pages when you push to the `main` branch. Make sure GitHub Pages is enabled in your repository settings.

### Azure Static Web Apps

To deploy to Azure Static Web Apps:

1. Create an Azure Static Web App in the Azure portal
2. Connect it to your GitHub repository
3. Configure the build settings:
   - **App location**: `/`
   - **Api location**: (leave empty)
   - **Output location**: `site`
4. Add a build command in the Azure portal: `pip install -r requirements.txt && mkdocs build`

## Project Structure

```
Improved-engine/
├── docs/                      # Documentation source files
│   ├── index.md              # Home page
│   ├── contact.md            # Contact page
│   ├── blog/                 # Blog section
│   │   ├── index.md         # Blog landing page
│   │   └── posts/           # Blog posts
│   ├── images/              # Image assets
│   └── stylesheets/         # Custom CSS
│       └── extra.css        # Gradient theme styles
├── .github/
│   └── workflows/           # GitHub Actions workflows
├── mkdocs.yml              # MkDocs configuration
├── requirements.txt        # Python dependencies
└── README.md              # This file
```

## Adding Blog Posts

1. Create a new Markdown file in `docs/blog/posts/`
2. Add frontmatter and content with a hero image:

```markdown
# Your Post Title

<div class="hero-image" style="background-image: url('IMAGE_URL');">
  <div class="hero-content">
    <h1>Post Title</h1>
    <p>Subtitle</p>
  </div>
</div>

Your content here...
```

3. Update `docs/blog/index.md` to link to your new post
4. Update the navigation in `mkdocs.yml` if needed

## Customization

### Changing Colors

Edit the CSS variables in `docs/stylesheets/extra.css`:

```css
:root {
  --gradient-primary: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  --gradient-secondary: linear-gradient(135deg, #f093fb 0%, #f5576c 100%);
}
```

### Modifying Theme

Edit `mkdocs.yml` to customize:
- Navigation structure
- Theme colors
- Features and plugins
- Social links

### Hero Images

Replace the Unsplash URLs in the Markdown files with your own images. You can:
- Use your own hosted images
- Use a CDN
- Place images in `docs/images/` and reference them locally

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is open source and available under the [MIT License](LICENSE).

## Support

If you encounter any issues or have questions, please [open an issue](https://github.com/Shanshan-Qu/Improved-engine/issues) on GitHub.

---

Built with ❤️ using [MkDocs](https://www.mkdocs.org/) and [Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)