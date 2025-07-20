# Research Notes Website

A Jekyll-based website for organizing and sharing research paper notes, built to be hosted on GitHub Pages.

## 🚀 Quick Start

### 1. Fork & Clone
```bash
# Fork this repository on GitHub, then clone your fork
git clone https://github.com/dmund95/ResearchNotes.git
cd ResearchNotes
```

### 2. Customize Configuration
Edit `_config.yml` to personalize your site:
```yaml
title: Your Research Notes
author: Your Name
email: your.email@example.com
url: "https://dmund95.github.io"
baseurl: "/ResearchNotes"
```

### 3. Deploy to GitHub Pages
1. Go to your repository settings on GitHub
2. Scroll down to "Pages" section
3. Set source to "Deploy from a branch"
4. Select "main" branch and "/ (root)" folder
5. Click "Save"

Your site will be available at: `https://dmund95.github.io/ResearchNotes`

## 📁 Structure

```
├── _config.yml          # Site configuration
├── _layouts/            # Page templates
│   ├── default.html     # Main layout
│   ├── topic.html       # Topic page layout
│   └── paper.html       # Research paper layout
├── _topics/             # Research topic pages
│   ├── machine-learning.md
│   └── computer-vision.md
├── _papers/             # Individual research papers
│   ├── attention-is-all-you-need.md
│   └── bert-paper.md
├── assets/css/          # Styling
│   └── style.scss
├── index.md             # Homepage
└── README.md           # This file
```

## ✍️ Adding Content

### Adding a New Topic
Create a new file in `_topics/` folder:

```yaml
---
layout: topic
title: "Your Topic Name"
description: "Brief description of the research area"
papers:
  - "paper-slug-1"
  - "paper-slug-2"
---

Content about this research topic...
```

### Adding a Research Paper
Create a new file in `_papers/` folder:

```yaml
---
layout: paper
title: "Paper Title"
authors: ["Author 1", "Author 2"]
year: 2023
journal: "Conference/Journal Name"
doi: "10.xxxx/xxxx"
topic: "machine-learning"
tags: ["tag1", "tag2"]
key_points:
  - "Key finding 1"
  - "Key finding 2"
---

Your detailed notes about the paper...
```

## 🎨 Customization

### Styling
- Edit `assets/css/style.scss` to customize appearance
- Modify CSS variables at the top for color scheme
- Responsive design included

### Navigation
- Update `_config.yml` navigation section
- Add new pages as needed

### Features
- Responsive design
- SEO optimization
- Tag system
- Cross-linking between papers and topics
- Clean, academic-friendly design

## 🔧 Local Development

To test your site locally:

```bash
# Install dependencies
bundle install

# Serve the site locally
rbenv rehash && bundle exec jekyll serve

# View at http://127.0.0.1:4000/ResearchNotes/
```

### Dependencies
- Ruby
- Jekyll
- GitHub Pages gem

## 📝 Content Guidelines

### Paper Notes Should Include:
- Complete citation information
- Key contributions and findings
- Methodology summary
- Personal insights
- Relevant tags

### Topic Pages Should Include:
- Overview of the research area
- List of related papers
- Key concepts and trends
- Future directions

## 🚀 Advanced Features

### Collections
The site uses Jekyll collections for topics and papers, enabling:
- Automatic cross-referencing
- Structured metadata
- Flexible organization

### SEO
Built-in SEO optimization with:
- Meta descriptions
- Open Graph tags
- Structured data
- Sitemap generation

## 📚 Examples

The repository includes example content:
- Machine Learning topic with Transformer and BERT papers
- Computer Vision topic (template)
- Properly formatted paper notes

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Add your content
4. Submit a pull request

## 📄 License

This template is open source and available under the MIT License.

## 🔗 Links

- [GitHub Pages Documentation](https://docs.github.com/en/pages)
- [Jekyll Documentation](https://jekyllrb.com/docs/)
- [Markdown Guide](https://www.markdownguide.org/)

---

**Happy researching!** 📖✨ 

## 🏆 **Recommended: Use a Ruby Version Manager**

The best practice is to use **rbenv** (or **rvm**) to manage Ruby versions:

### Install rbenv (macOS):
```bash
# Install rbenv via Homebrew
brew install rbenv ruby-build

# Add to your shell profile (~/.zshrc)
echo 'eval "$(rbenv init - zsh)"' >> ~/.zshrc
source ~/.zshrc

# Install a Ruby version (Jekyll works well with 3.1.x)
rbenv install 3.1.4
rbenv local 3.1.4  # Set for this project only
```

Then run:
```bash
bundle install
bundle exec jekyll serve
```

## 🐳 **Alternative: Docker (Complete Isolation)**

If you want complete isolation, use Docker:

```bash
# Run Jekyll in a container
docker run --rm -it \
  -v "$PWD":/srv/jekyll \
  -p 4000:4000 \
  jekyll/jekyll:4 \
  bash -c "bundle install && bundle exec jekyll serve --host 0.0.0.0"
```

## ⚠️ **System Ruby + Bundler (Minimal Protection)**

If you just use system Ruby with Bundler:
- Bundler will install gems in your user directory (not system-wide)
- Some isolation, but less clean than rbenv
- Generally safe but not as organized

## **What I'd Recommend:**

1. **Use rbenv** - It's the Ruby community standard and gives you clean version isolation
2. Your `Gemfile` uses GitHub Pages gems, which are well-maintained and safe
3. Bundler already provides gem-level isolation even without rbenv

Would you like me to help you set up rbenv, or would you prefer to try one of the other approaches? 