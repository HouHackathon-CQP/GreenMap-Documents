# Contributing Guidelines

Thank you for your interest in contributing to GreenMap! This document provides guidelines and instructions for contributing to the project.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [How to Contribute](#how-to-contribute)
- [Development Workflow](#development-workflow)
- [Coding Standards](#coding-standards)
- [Commit Guidelines](#commit-guidelines)
- [Pull Request Process](#pull-request-process)
- [Reporting Issues](#reporting-issues)

## Code of Conduct

Please read and follow our [Code of Conduct](code-of-conduct.md). We are committed to providing a welcoming and inclusive environment for all contributors.

## Getting Started

### Prerequisites

Before you begin, make sure you have:

- Git installed on your machine
- Node.js (v14 or higher)
- Python (v3.8 or higher)
- A GitHub account
- Familiarity with Git and GitHub workflow

### Fork and Clone

1. Fork the GreenMap repository on GitHub
2. Clone your fork locally:

```bash
git clone https://github.com/YOUR_USERNAME/GreenMap.git
cd GreenMap
```

3. Add the upstream repository:

```bash
git remote add upstream https://github.com/HouHackathon-CQP/GreenMap.git
```

### Set Up Development Environment

1. Install dependencies:

```bash
npm install
pip install -r requirements.txt
```

2. Create a `.env` file:

```bash
cp .env.example .env
```

3. Run the development server:

```bash
npm run dev
```

## How to Contribute

### Types of Contributions

We welcome various types of contributions:

- 🐛 **Bug fixes** - Fix issues and improve stability
- ✨ **New features** - Add new functionality
- 📝 **Documentation** - Improve or add documentation
- 🎨 **Design** - UI/UX improvements
- 🧪 **Tests** - Add or improve test coverage
- ♻️ **Refactoring** - Code quality improvements
- 🌍 **Translations** - Add language support

### Areas to Contribute

Priority areas where we need help:

1. **Mobile App Development** - iOS and Android apps
2. **API Enhancements** - New endpoints and features
3. **Documentation** - User guides and API docs
4. **Accessibility** - Improve accessibility features
5. **Internationalization** - Add language translations
6. **Testing** - Increase test coverage
7. **Performance** - Optimization and improvements

## Development Workflow

### Creating a Branch

Create a feature branch from `main`:

```bash
git checkout main
git pull upstream main
git checkout -b feature/your-feature-name
```

Branch naming conventions:

- `feature/` - New features
- `fix/` - Bug fixes
- `docs/` - Documentation changes
- `refactor/` - Code refactoring
- `test/` - Test additions/changes

Examples:
- `feature/add-project-tags`
- `fix/map-rendering-issue`
- `docs/update-api-reference`

### Making Changes

1. Make your changes following our [coding standards](#coding-standards)
2. Test your changes thoroughly
3. Run linters and formatters:

```bash
npm run lint
npm run format
```

4. Run tests:

```bash
npm test
```

### Keeping Your Branch Updated

Regularly sync with upstream:

```bash
git fetch upstream
git rebase upstream/main
```

## Coding Standards

### JavaScript/TypeScript

We follow the Airbnb JavaScript Style Guide:

```javascript
// Good
const getUserName = (user) => {
  return user.name || 'Anonymous';
};

// Bad
function get_user_name(user) {
  return user.name || 'Anonymous'
}
```

Key points:
- Use `const` and `let`, not `var`
- Use arrow functions when appropriate
- Use template literals for string interpolation
- Add semicolons
- Use meaningful variable names

### Python

We follow PEP 8 style guide:

```python
# Good
def get_user_name(user):
    """Return the user's name or 'Anonymous'."""
    return user.name or 'Anonymous'

# Bad
def GetUserName(user):
    return user.name or 'Anonymous'
```

Key points:
- Use snake_case for functions and variables
- Use PascalCase for classes
- Add docstrings to functions
- Maximum line length: 88 characters (Black formatter)

### HTML/CSS

```html
<!-- Good -->
<div class="project-card">
  <h2 class="project-card__title">{{ title }}</h2>
  <p class="project-card__description">{{ description }}</p>
</div>

<!-- Bad -->
<div class="projectCard">
  <h2>{{ title }}</h2>
  <p>{{ description }}</p>
</div>
```

Key points:
- Use BEM naming convention
- Use semantic HTML
- Keep CSS modular
- Use CSS variables for theming

### Documentation

- Use clear, concise language
- Include code examples
- Add screenshots for UI changes
- Keep documentation up-to-date with code changes

## Commit Guidelines

We follow [Conventional Commits](https://www.conventionalcommits.org/):

### Commit Message Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Types

- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, etc.)
- `refactor`: Code refactoring
- `test`: Test additions/changes
- `chore`: Build process or auxiliary tool changes

### Examples

```
feat(projects): add tag filtering functionality

Add ability to filter projects by tags on the map interface.
Users can now select multiple tags to refine their search.

Closes #123
```

```
fix(api): resolve rate limiting issue

Fix incorrect rate limit calculation that was causing
premature throttling for enterprise accounts.

Fixes #456
```

```
docs(api): update authentication examples

Add examples for Bearer token authentication and clarify
the API key generation process.
```

### Best Practices

- Use imperative mood ("add feature" not "added feature")
- First line should be 50 characters or less
- Reference issues and pull requests in the footer
- Use body to explain what and why, not how

## Pull Request Process

### Before Submitting

Checklist before creating a PR:

- [ ] Code follows project style guidelines
- [ ] Tests pass locally
- [ ] New tests added for new functionality
- [ ] Documentation updated
- [ ] Commits follow conventional format
- [ ] Branch is up-to-date with main

### Creating a Pull Request

1. Push your branch to your fork:

```bash
git push origin feature/your-feature-name
```

2. Create a PR on GitHub with a clear title and description

### PR Template

Use this template for your PR description:

```markdown
## Description
Brief description of the changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Documentation update
- [ ] Refactoring

## Related Issues
Closes #123

## Testing
Describe how you tested the changes

## Screenshots (if applicable)
Add screenshots for UI changes

## Checklist
- [ ] Code follows style guidelines
- [ ] Tests pass
- [ ] Documentation updated
- [ ] Self-review completed
```

### Review Process

1. At least one maintainer must approve
2. All CI checks must pass
3. Resolve any requested changes
4. Once approved, a maintainer will merge

### After Your PR is Merged

1. Delete your branch:

```bash
git branch -d feature/your-feature-name
git push origin --delete feature/your-feature-name
```

2. Update your local main:

```bash
git checkout main
git pull upstream main
```

## Reporting Issues

### Before Creating an Issue

1. Search existing issues
2. Check if it's already fixed in `main`
3. Gather relevant information

### Bug Reports

Include the following:

```markdown
## Bug Description
Clear description of the bug

## Steps to Reproduce
1. Go to '...'
2. Click on '...'
3. See error

## Expected Behavior
What should happen

## Actual Behavior
What actually happens

## Environment
- OS: [e.g., Windows 10]
- Browser: [e.g., Chrome 96]
- Version: [e.g., 1.2.3]

## Screenshots
If applicable

## Additional Context
Any other relevant information
```

### Feature Requests

Include the following:

```markdown
## Feature Description
Clear description of the proposed feature

## Use Case
Why is this feature needed?

## Proposed Solution
How should it work?

## Alternatives Considered
Other approaches you've thought about

## Additional Context
Any other relevant information
```

## Communication

### Where to Ask Questions

- **General questions**: GitHub Discussions
- **Bug reports**: GitHub Issues
- **Feature requests**: GitHub Issues
- **Security issues**: security@greenmap.example.com
- **Real-time chat**: Discord server

### Response Times

- We aim to respond to issues within 48 hours
- PR reviews typically take 3-5 business days
- Security issues are addressed immediately

## Recognition

Contributors are recognized in several ways:

- Listed in CONTRIBUTORS.md
- Mentioned in release notes
- Featured on our website
- Special badges for significant contributions

## License

By contributing to GreenMap, you agree that your contributions will be licensed under the same license as the project (see LICENSE file).

## Getting Help

Need help with contributing?

- Read our [Getting Started Guide](../getting-started/quick-start.md)
- Check out [good first issues](https://github.com/HouHackathon-CQP/GreenMap/labels/good%20first%20issue)
- Join our Discord for real-time help
- Email us at contribute@greenmap.example.com

---

*Thank you for contributing to GreenMap! Together, we're making a positive impact!* 🌍💚
