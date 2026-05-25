---
title: "Building This Website: How I Set Up My Personal Site"
date: 2026-05-24
draft: false
tags: ["hugo", "cloudflare", "webdev"]
---

## Welcome

If you are reading this, my website is operational — and that is already a win! This first post is going to walk through how I built this website from scratch, why I built it, and what I plan to do with it going forward.

## Why I Built This

I recently finished my bachelor's degree in cybersecurity and am currently wrapping up my master's. Over the course of those programs I have worked on a lot of projects, explored a lot of topics, and learned a massive amount — most of which lives scattered across notes, files, and my own memory. I wanted a central place to document and show off that work in a way that is organized, public, and actually mine. This site is that central location for me to share what I have learned, the mistakes I have made along the way and some cool projects I am working on.

## How Did I Make this Website?

The site is built using a static site generator called **Hugo** paired with the **Hextra** theme, and hosted for free on **Cloudflare Pages**.

Here is a quick breakdown of each piece:

**Hugo** is an open source static site generator written in Go. Instead of a database or a server rendering pages on the fly, Hugo takes Markdown files and templates and compiles them into plain HTML, CSS, and JavaScript. The result is a site that is extremely fast, cheap to host, and simple to maintain. Writing a new post is as easy as creating a Markdown file and pushing it to GitHub.

**Hextra** is the Hugo theme I chose. It gives the site its dark mode layout, navigation, and overall structure. I customized the homepage layout significantly using raw HTML and CSS to get the profile card, photo, and section cards looking the way I wanted.

**Cloudflare Pages** handles the hosting. Every time I push a change to my GitHub repository, Cloudflare automatically pulls the latest code, runs the Hugo build, and deploys the updated site within about a minute. The hosting itself is completely free (unless you want a custonm domain name), and Cloudflare's global network means the site loads fast for anyone visiting from anywhere.

The domain `ericantonecchia.com` will be pointed here once I register it. For now the site lives at `ericantonecchia.pages.dev`.

## The Tech Stack at a Glance

- **Static site generator:** Hugo v0.161.1 (Extended)
- **Theme:** Hextra
- **Content format:** Markdown
- **Version control:** Git + GitHub
- **Hosting:** Cloudflare Pages
- **OS during development:** Windows 11
- **Editor:** VS Code

## How the Workflow Works

Once everything was set up, the day to day workflow for publishing something new is just three commands:

```powershell
git add .
git commit -m "New post"
git push
```

Cloudflare picks up the push automatically and the site is updated within a minute. No servers to manage, no CMS to log into, no deployment scripts to run manually.

## What I Plan to Do With This Site

This site is going to serve a few purposes.

**Showcasing projects.** Whether it is something I built for a class, a CTF challenge I worked through, a tool I wrote, or something I am just exploring on my own — I want a place to write it up properly and share it. A GitHub repo is great for code, but sometimes the more valuable thing is the explanation of the thinking behind it.

**Cybersecurity topics.** I find a lot of topics  in this field genuinely interesting and worth writing about. That might be a breakdown of a vulnerability, notes on a tool, a writeup from a competition, or just something I read that I thought deserved more attention.

**Homelab documentation.** This is the one I am most excited about. I am in the early stages of setting up a homelab — a personal lab environment built on my own hardware at home, used for learning, experimenting, and building things in a safe controlled space. Homelabs are common in the cybersecurity and IT world because they give you a place to practice skills that are difficult to develop otherwise: network configuration, server administration, virtualization, self-hosted services, security monitoring, and more.

I will be documenting the homelab build from the ground up as I go — hardware choices, software decisions, things that break, things that work, and what I learn along the way.

## Wrapping Up

This site is a work in progress and will keep evolving as I add to it. If you are reading this and want to connect, my LinkedIn are and email are provided on the homepage.

This is just the beginning, more posts coming soon!