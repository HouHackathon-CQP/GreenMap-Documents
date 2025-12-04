# GreenMap Documentation

Welcome to the official documentation repository for the GreenMap project!

## 📚 About

This repository contains the complete documentation for GreenMap, an innovative platform designed to connect people with environmental initiatives and promote sustainable actions in communities worldwide.

## 🚀 Quick Start

### Prerequisites

- Python 3.8 or higher
- pip

### Installation

1. Clone this repository:
   ```bash
   git clone https://github.com/HouHackathon-CQP/GreenMap-Documents.git
   cd GreenMap-Documents
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

### Building the Documentation

Build the static site:
```bash
mkdocs build
```

The built site will be in the `site/` directory.

### Development Server

Run a local development server with live reloading:
```bash
mkdocs serve
```

Then open your browser to `http://localhost:8000`

## 📖 Documentation Structure

```
docs/
├── index.md                    # Home page
├── getting-started/
│   ├── introduction.md         # Introduction to GreenMap
│   ├── installation.md         # Installation guide
│   └── quick-start.md          # Quick start guide
├── user-guide/
│   ├── overview.md             # User guide overview
│   └── features.md             # Detailed features
├── api-reference/
│   ├── overview.md             # API overview
│   └── endpoints.md            # API endpoints reference
├── contributing/
│   ├── guidelines.md           # Contributing guidelines
│   └── code-of-conduct.md      # Code of conduct
└── about.md                    # About GreenMap
```

## 🛠️ Technologies

- **[MkDocs](https://www.mkdocs.org/)** - Static site generator
- **[Material for MkDocs](https://squidfunk.github.io/mkdocs-material/)** - Material Design theme
- **[PyMdown Extensions](https://facelessuser.github.io/pymdown-extensions/)** - Markdown extensions

## 🤝 Contributing

We welcome contributions to the documentation! Please read our [Contributing Guidelines](docs/contributing/guidelines.md) before submitting a pull request.

### How to Contribute

1. Fork this repository
2. Create a new branch (`git checkout -b docs/your-feature`)
3. Make your changes
4. Test locally with `mkdocs serve`
5. Commit your changes (`git commit -m 'Add some documentation'`)
6. Push to the branch (`git push origin docs/your-feature`)
7. Open a Pull Request

## 📝 Documentation Guidelines

When contributing to documentation:

- Use clear, concise language
- Include code examples where appropriate
- Add screenshots for UI-related documentation
- Test all links and code snippets
- Follow the existing structure and style
- Run `mkdocs build --strict` to check for errors

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🌍 Links

- **Main Project**: [GreenMap](https://github.com/HouHackathon-CQP/GreenMap)
- **Documentation Site**: [GreenMap Docs](https://houhackathon-cqp.github.io/GreenMap-Documents/)
- **Community**: [Discord](https://discord.gg/greenmap)

## 💚 Support

If you need help or have questions:

- Open an [issue](https://github.com/HouHackathon-CQP/GreenMap-Documents/issues)
- Join our [Discord community](https://discord.gg/greenmap)
- Email us at support@greenmap.example.com

---

*Making environmental action accessible to everyone!* 🌍💚