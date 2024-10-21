
# PSEO (Programmatic SEO Tool)

PSEO is a powerful command-line tool designed for programmatic SEO, enabling you to generate, optimize, and manage bulk SEO-optimized pages efficiently.

## Table of Contents

1. [Overview](#overview)
2. [Installation](#installation)
3. [Configuration](#configuration)
4. [Usage](#usage)
   - [Initializing a Project](#initializing-a-project)
   - [Generating Bulk Pages](#generating-bulk-pages)
   - [Creating Sample Data](#creating-sample-data)
   - [Previewing Generated Content](#previewing-generated-content)
   - [Generating an Industry Glossary](#generating-an-industry-glossary)
   - [Pattern-Based Pages Generation](#pattern-based-pages-generation)
5. [AI-Powered Content Generation](#ai-powered-content-generation)
6. [Command Reference](#command-reference)
7. [Configuration File](#configuration-file)
8. [Contributing](#contributing)
9. [License](#license)

## Overview

PSEO streamlines the process of creating large-scale, SEO-optimized content for websites. Key features include:

- Bulk page generation based on templates and data sources
- AI-powered content creation for unique, relevant pages
- Industry-specific glossary generation
- Local server for content preview
- Flexible configuration options for various SEO strategies
- Pattern-based pages generation for scalable content creation

Ideal for SEO professionals, content marketers, and website owners looking to scale their content efficiently.

## Installation

To install PSEO globally on your system:

```bash
# Clone the repository
git clone https://github.com/c7-labs/programtic-seo
cd pseo

# Install dependencies
npm install

# Install the CLI globally
sudo npm install -g .
```

After installation, you can use the `pseo` command from anywhere in your terminal.

## Configuration

For AI-powered features, set up the following environment variables:

```bash
export OPENAI_API_KEY='your-openai-api-key'
export EXA_API_KEY='your-exa-api-key'
```
Add the following environment variable if you want to use Tavily for reference links
```bash
export TAVILY_API_KEY='your-tavily-api-key'
```

Add these to your `.bashrc` or `.zshrc` file for permanent configuration.

## Usage

### Initializing a Project

Start a new PSEO project:
```bash
pseo --init --projectName=myProject
```

### Creating Sample Data

Generate sample data for testing your page templates:
```bash
pseo --fake
```
This creates a `fake.json` file with sample data structures. Update config.yaml to generate with this fake data. 

### Generating Bulk Pages

Generate SEO-optimized pages based on your configuration:
```bash
pseo --gen
```

Ensure your `config.yaml` file is set up with your desired page structure, templates, and data sources.

### Previewing Generated Content

Start a local server to preview your generated pages:
```bash
pseo --serve
```

### Generating an Industry Glossary

Create a comprehensive, SEO-friendly industry glossary:
```bash
pseo --glossary --industry=Cybersecurity --skipCategories --numberOfTerms=100
```

### Generating Reference Links via Tavily

Generate reference links using Tavily:
```bash
pseo --glossary --industry=Cybersecurity --skipCategories --numberOfTerms=100 --tavily 
```

### Pattern-Based Pages Generation

Generate pages based on custom patterns:
```bash
pseo --pattern --dataFile=data.json --headingPatternFile=heading_pattern.txt --outlinePatternFile=outline_pattern.txt --outputFile=result.json
```

This feature allows you to create structured pages using predefined patterns for headings and outlines. It's particularly useful for generating large sets of similar pages with varying content based on your data.

## AI-Powered Content Generation

PSEO leverages AI to generate high-quality, unique content for your bulk pages and glossaries:

1. Ensure you've set up the required API keys (see [Configuration](#configuration)).
2. Use the `--glossary` command with desired options for industry-specific content.
3. Use the `--pattern` command for pattern-based pages generation, which creates full page structures including headings, outlines, and content.
4. Customize AI prompts in your config file for tailored page content generation.

The AI generates terms, definitions, and related content based on your specified patterns and data, ensuring each page is unique and valuable for SEO.

## Command Reference

Quick reference for PSEO commands:

```
Usage:
  --init                        Initialize project
    --projectName               Project name [Mandatory]
    Example                     pseo --init --projectName=MyProject

  --gen                         Generate the pages
    Example                     pseo --gen

  --fake                        Generate fake data
    Example                     pseo --fake

  --serve                       Start the server
    Example                     pseo --serve

  --glossary                    Generate glossary
    --industry=<name>           Pass industry name [Mandatory]
    --termsFile=<file>          Pass terms file [Optional]
    --numberOfTerms=<number>    Number of terms [Optional]
    --skipCategories            Skip categories [Optional]
    Example:                    pseo --glossary --industry=Cybersecurity --skipCategories --numberOfTerms=4

  --pattern                     Generate pattern-based headings and outlines
    --dataFile=<file>           JSON file containing data for pattern generation [Mandatory]
    --headingPatternFile=<file> File containing the pattern for generating headings [Mandatory]
    --outlinePatternFile=<file> File containing the pattern for generating outlines [Mandatory]
    --outputFile=<file>         File to save generated headings and outlines as JSON [Optional, default: output.json]
    Example:                    pseo --pattern --dataFile=data.json --headingPatternFile=heading_pattern.txt --outlinePatternFile=outline_pattern.txt --outputFile=result.json

Note: The OpenAI API key should be set as an environment variable named OPENAI_API_KEY.
```

For detailed information about each command and its options, run `pseo` without arguments.

## Configuration File

PSEO uses a YAML configuration file to customize the behavior of the tool and the structure of the generated pages. Here's an explanation of the key fields in the `config.yaml` file:

```yaml
---
projectName: "myproject"
jsonFilePath: "./input.json"
baseUrl: https://example.com/example
portalHeading: Welcome to Digital Marketing Glossary
portalDescription: Navigate the complex world of digital marketing with ease. Our comprehensive glossary covers essential terms and concepts, from SEO and PPC to social media metrics and email marketing strategies. Whether you're a beginner or a seasoned professional, find clear, concise definitions to enhance your digital marketing knowledge and stay ahead in the ever-evolving online landscape.
portalTitle: Digital Marketing Glossary
searchPlaceholder: Search Term, e.g. On Page SEO
useAlphabetsCategory: true
homeLink: https://example.com/
logoLink: "/example"
logoImgUrl: https://example.com/gracker-logo.png
ctaLink: https://portal.gracker.ai/
copyrightText: "© 2024 Example. Made with ❤️ in San Francisco."
faviconUrl: https://example.com/favicon.ico
pagesTitle:
  prefix: 'Digital Marketing Glossary - '
  suffix: " - Example"
categoryPagesTitle:
  prefix: ''
  suffix: ''
templateRoot:
- "./templates/"
homeTemplatePath: "./templates/homePageTemplate.ejs"
categoryTemplatePath: "./templates/categoryTemplate.ejs"
pageTemplatePath: "./templates/pagesTemplate.ejs"
outputDir: "./output"
```

### Key Configuration Fields:

- `projectName` : Name of your project
- `jsonFilePath`: Path to the JSON file containing your glossary data.
- `baseUrl`: The base URL for your generated pages.
- `portalHeading`, `portalDescription`, `portalTitle`: Metadata for the main glossary page.
- `searchPlaceholder`: Placeholder text for the search input.
- `useAlphabetsCategory`: Whether to categorize terms alphabetically.
- `homeLink`, `logoLink`, `logoImgUrl`: Navigation and branding settings.
- `ctaLink`: Call-to-action link.
- `copyrightText`: Copyright information for the footer.
- `faviconUrl`: URL for the favicon.
- `pagesTitle`, `categoryPagesTitle`: Prefix and suffix for page titles.

### Template Configuration (Commented Out by Default):
- `templateRoot`: Directories to look for partial templates.
- `homeTemplatePath`, `categoryTemplatePath`, `pageTemplatePath`: Paths to specific EJS templates.
- `outputDir`: Directory where generated pages will be saved.

To use custom templates, uncomment and adjust these paths as needed.

### Customizing Your Configuration
1. Copy the default `config.yaml` file to your project root.
2. Modify the values to match your project's requirements.
3. Ensure all paths (e.g., `jsonFilePath`, template paths) are correct relative to your project structure.
4. Run `pseo --gen` to apply the configuration and generate your pages.

## Contributing

Contributions are welcome! Please read our [contributing guidelines](CONTRIBUTING.md) before submitting a pull request.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details.
