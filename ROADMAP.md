# versionChecker — Roadmap

## Current Status

versionChecker is functional for its core purpose: scraping latest versions, comparing against inventory, and generating risk review tickets. The primary known improvement area is inventory management — the current approach works but has room to grow.

---

## Known Friction

### Inventory Management
The inventory table is currently a flat file. It works, but updating and maintaining it is a manual step. Running scripts directly against the shared drive is not an acceptable path — so improving inventory management requires a different approach.

---

## Future Directions

Two viable paths forward, not mutually exclusive:

### Option 1 — GitLab Integration
Use GitLab to host and manage the inventory, leveraging existing infrastructure the team already has access to. Version check results and inventory updates could be tracked alongside other AppSec tooling work without introducing a new dependency.

### Option 2 — Analyst Dashboard Integration (Preferred Long-Term)
A dedicated analyst dashboard with a web instance is planned for the AppSec group. versionChecker is a natural fit for a dedicated tool within that dashboard, which would include:

- Inventory displayed and managed in the dashboard UI
- Current version check results visible at a glance
- Last run timestamp
- On-demand version check trigger
- Risk review ticket launch from within the dashboard
- Update ticket status tracking

This path consolidates versionChecker's functionality into a purpose-built interface alongside other AppSec tooling, rather than maintaining it as a standalone script.

---

## What's Not on the Roadmap

- **Scripts running within the shared drive** — not an acceptable approach regardless of the inventory solution chosen.
- **Automated download or installation** — versionChecker's role is detection and ticket initiation only. Software delivery remains a controlled, human-approved process by design.
