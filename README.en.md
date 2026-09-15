# dsh-helper — Unlimited parallel dsh instances on one desktop

[中文](README.md) · [User Guide](docs/user-guide.en.md) · [Releases](https://github.com/x102201/dsh-helper/releases)

![Demo](docs/assets/video/dsh-helper-demo.gif)

[Download full demo (mp4)](docs/assets/video/dsh-helper-demo.mp4)

I run several lines of business in parallel. Out of the box you get one dsh; packing every capability into the same workspace creates conflicts — so I built this:
**One desktop window. Unlimited isolated DeepSeek Harness runtimes in parallel. Each instance = a full, separate dsh.**

---

## 1. Isolate: one dsh cannot carry two workloads

### Pain

I run three lines of business in parallel: customer messages, code, and tests plus reports.

Default is one dsh (one `DSH_HOME`). Install every plugin into the same workspace and the tool list grows until the model starts picking the wrong tools — not a configuration mistake, but three unrelated capability sets forced into one preset. **Structurally, it cannot carry them.**

Agent presets cannot split that load: **only one mounts per session**, and switching after a turn is locked.

> Per DeepSeek Harness: [*Agent Presets and Personas*](https://deepseekdocs.com/en/docs/features/persona) · [architecture note *A session's agent is composed from a preset*](https://github.com/deepseek-ai/deepseek-harness/blob/master/.agents/notes/implemented/architecture/2026-08-03-per-session-agent-presets.md)

### Fix

Do not concentrate every workload in one dsh.
**Each instance = one full, separate dsh** (own process, port, and `DSH_HOME`) — not a tab inside a single runtime.

Support on the left, coding on the right, tests below — run as many as you need; plugins never conflict.

![Split layout](docs/assets/en/screenshot-main-light.png)

> Isolation makes each runtime independent. Real business is not three non-intersecting lines —
> a change on the customer side still has to reach development. That is section 2.

---

## 2. Collaborate: dedicated instances, one workspace

**Each dsh is a dedicated instance:** support, development, and testing each own one workload. Plugins are isolated per instance — that was section 1.

But the three instances advance the same delivery. Splitting them across three computers means 3× hardware, scattered directories, and no shared workspace. **Dedicated instances need to run in parallel in one workspace, not one instance per machine.**

Run them on one computer: **three instances share one project directory**; plugins stay isolated, files are shared. Dispatch from the split panes — commit on the left, update the same docs on the right, verify against the checklist below.

This is not three unrelated windows side by side. It is three dedicated instances in one workspace advancing **the same version**.

![Dedicated instances: one workspace vs one instance per machine](docs/assets/en/collab-model.svg)

---

## 3. Deliver: configure several instances, export several packs

**The environment is the product; export is delivery.**

It took days to get the support, development, and testing dedicated instances running together — plugins, presets, and flow aligned step by step.

Then it has to be delivered. What breaks is not “can they use it”, but that **every delivery feels like rebuilding the project**:

1. **Cannot reproduce** — days later even you cannot say which plugins and which preset are this set; deploy for someone else and it drifts, another few days gone
2. **Cannot deliver** — a README never installs cleanly; copying the folder invites uncontrolled redistribution
3. **Cannot scale** — customer two and three need the same remote deploy; **deploy time dwarfs configuration time**, so delivery does not scale

**`.dshpack`:** export that one configured instance (one full dsh) as a file. Import and run. Bind machine code / password; forbid re-export — you deliver a finished product, not deployment labor.

Configure several dedicated instances, export several packs. One `.dshpack` is still one dsh; after import it shows up in the sidebar — the workspace layout is arranged by the recipient.

![Package flow](docs/assets/en/dshpack-flow.svg)

---

## User guide

1. [Concepts](docs/user-guide.en.md#concepts)
2. [Install](docs/user-guide.en.md#install)
3. [First run](docs/user-guide.en.md#first-run)
4. [Workspaces](docs/user-guide.en.md#workspaces)
5. [Packages (.dshpack)](docs/user-guide.en.md#packages-dshpack)
6. [Data, migrate, uninstall](docs/user-guide.en.md#data-migrate-uninstall)
7. [Settings reference](docs/user-guide.en.md#settings-reference)
8. [Troubleshooting](docs/user-guide.en.md#troubleshooting)
