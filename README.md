# versionChecker

## Overview

versionChecker is a lightweight Python web scraper that monitors latest release versions for AppSec tooling and compares them against an internal inventory. When newer versions are detected, it automates the creation of a risk review ticket — initiating the org's controlled software delivery process, where approved software is downloaded externally and placed in a shared network location for the AppSec team to copy over.

---

## The Problem It Solves

AppSec tooling (Kali Linux, Burp Suite, Burp extensions) cannot be downloaded directly on the internal network. Updates go through a risk review and approval process — but someone has to notice a new version exists and kick that process off. versionChecker automates the detection step and generates the ticket, so updates don't get missed and the review process starts without manual monitoring.

---

## How It Works

### 1. Inventory Read
versionChecker reads the inventory table, which tracks the currently approved/installed version of each monitored tool.

### 2. Version Scraping
For each tool in the inventory, versionChecker scrapes the relevant page for the latest version number:

| Tool | Source |
|------|--------|
| Kali Linux | Kali Linux releases page |
| Burp Suite | PortSwigger Burp Suite page |
| Burp Extensions | BApp Store (specific HTML element containing version number) |

### 3. Comparison
Scraped latest versions are compared against inventoried versions. Tools where the latest version exceeds the inventoried version are flagged.

### 4. Risk Review Ticket
For each flagged tool, versionChecker creates a risk review ticket in the ticketing system. The ticket initiates the org's approval process — once approved, the software is downloaded externally and placed in a shared network location for the AppSec team to copy over.

---

## Key Features

- **Targeted scraping** — pulls version numbers from specific HTML elements on vendor/release pages
- **Inventory-driven** — comparison is based on what the org currently has approved, not just what's installed
- **Automated ticket creation** — no manual ticket writing when updates are detected
- **Controlled delivery alignment** — designed around the org's process; does not attempt to download or install anything

---

## Requirements

- Ticketing platform API token
- Internet access for scraping (Kali releases page, PortSwigger, BApp Store)

---

## File Structure

```
versionChecker/
├── versionchecker.py     # Core scraping and comparison logic
├── [ticket.py]           # Ticket creation script (if separate)
└── inventory.csv/xlsx    # Tracked tools and current approved versions
```
