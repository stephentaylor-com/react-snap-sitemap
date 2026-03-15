# react-snap-sitemap

Fork of @arcadian-group/react-snap-sitemap — a CLI tool that generates `sitemap.xml` from the pre-rendered HTML output of react-snap. Scans the `build/` directory for `index.html` files and creates a valid XML sitemap with configurable base URL, change frequency, and URL exclusions.

## How It Works

After react-snap pre-renders your React app into static HTML files in `build/`, this tool recursively scans the directory structure, finds all `index.html` files, converts their paths to URLs, and generates a standards-compliant `sitemap.xml`.

## Usage

```bash
npx react-snap-sitemap --base-url=https://yoursite.com/
```

### CLI Options

| Flag | Description | Default |
|------|-------------|---------|
| `--base-url=URL` | **Required.** Base URL for all sitemap entries | — |
| `--change-frequency=freq` | Change frequency hint (daily, weekly, monthly, yearly) | `monthly` |
| `--black-list=url1,url2` | Comma-separated URLs to exclude from sitemap | — |
| `--add-slash=true` | Append trailing slashes to all URLs | `false` |

### Example

```bash
npx react-snap-sitemap \
  --base-url=https://example.com/ \
  --change-frequency=weekly \
  --black-list=https://example.com/admin,https://example.com/draft
```

## Features

- Recursively scans `build/` for pre-rendered pages
- Excludes 404 pages automatically
- Sorts URLs by length (shortest first)
- Sets priority 1.0 for homepage, 0.5 for all other pages
- Uses current date as `lastmod` for all entries
- Outputs `build/sitemap.xml` in UTF-8

## Tech Stack

- **xmlbuilder** 15.1 for XML generation
- Node.js >= 8.6

## Setup

```bash
npm install @alex-drocks/react-snap-sitemap
```

Or add to your build pipeline:

```json
{
  "scripts": {
    "postbuild": "react-snap && react-snap-sitemap --base-url=https://yoursite.com/"
  }
}
```
