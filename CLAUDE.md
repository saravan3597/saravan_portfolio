# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a static personal portfolio website for Saravan Somanchi, a Senior Software Engineer. It is a single-page application with no build step or package manager — just plain HTML, CSS, and vanilla JavaScript.

## Running Locally

Open `index.html` directly in a browser, or serve it with any static file server:

```bash
python3 -m http.server 8080
# then visit http://localhost:8080
```

## Docker

The site is containerized with nginx:

```bash
docker build -t saravan-portfolio .
docker run -p 8080:80 saravan-portfolio
# then visit http://localhost:8080
```

## Architecture

Three files make up the entire site:

- **`index.html`** — all content and structure; contains an inline `<script>` block at the bottom handling dark/light theme toggle (persisted via `localStorage`) and mobile nav auto-close logic
- **`style.css`** — all styling via CSS custom properties (`--clr-*`, `--spacing-*`, `--font-size-*`); dark mode is implemented by toggling `[data-theme="dark"]` on `<html>`; layout uses CSS Grid and Flexbox with no frameworks
- **`assets/profile-pic.jpg`** — profile photo

## Theme System

Light/dark theme is driven entirely by CSS variables. The `[data-theme="dark"]` attribute on `<html>` switches the variable set. The toggle button reads/writes `localStorage` key `"theme"` and falls back to `prefers-color-scheme` media query on first visit.

## Sections

The page has five anchor-linked sections: `#experience`, `#skills`, `#education`, `#certifications`, `#contact`. The `#certifications` section is nested inside the `#education` section's container.

## Deployment

The site is deployed as a static site. The Dockerfile copies all files into nginx's default HTML directory and exposes port 80.
