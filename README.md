# Stockwatcher

![Stockwatcher in the browser: a live heat map of the 100 shares r/wallstreetbets mentions most, grouped by sector and sized by market value](assets/screenshot.jpg)

**Read the story behind it:** [Building personalised skills](https://msukhareva.substack.com/p/building-personalised-skills-an-agentic) on the AI Realist Substack.

A live stock-market dashboard and heat map in the browser, steered from the chat.
Ask for an index, a sector, a theme, companies, an investor's 13F portfolio, what
r/wallstreetbets is discussing, or a question about companies that needs research.

It learns as you use it: say "this is my portfolio: 10 AAPL, 5 MSFT" once and "show my
portfolio" brings it back ("add 5 TSLA to my portfolio" and "I sold 2 AAPL" change it);
researched answers are remembered; and the page offers your usual requests as buttons.

Built by [Maria Sukhareva](https://www.linkedin.com/in/msukhareva/) of
[AI Realist](https://airealist.org).

- Stockwatcher on ClawHub: [clawhub.ai/ktoetotam/plugins/stockwatcher](https://clawhub.ai/ktoetotam/plugins/stockwatcher) (the plugin for OpenClaw)
- AI Realist: [airealist.org](https://airealist.org/?utm_source=github) (courses, workshops and registrations)
- The article: [Building personalised skills](https://msukhareva.substack.com/p/building-personalised-skills-an-agentic) (how and why Stockwatcher was built)

## What you need

- Windows, macOS or Linux.
- [Node.js](https://nodejs.org) 18 or newer (the "LTS" installer, default choices). That is
  the only thing to install: there are no packages to download, no accounts and no API keys.

Prices come from Yahoo Finance (Nasdaq when Yahoo is busy) and can be delayed. Not
investment advice.

## Install

The same plugin works in Claude Code, Codex and OpenClaw.

**Claude Code** (type these in the chat):

```bash
/plugin marketplace add ktoetotam/stockwatcher-plugin
/plugin install stockwatcher@stockwatcher
```

**Codex** (type these in a terminal, then start a new chat):

```bash
codex plugin marketplace add ktoetotam/stockwatcher-plugin
codex plugin add stockwatcher@airealist
```

In the Codex or ChatGPT desktop app you can instead add the marketplace with the first
command and install Stockwatcher from the Plugins Directory.

**OpenClaw** (in a terminal; it loads in new chats after the Gateway restarts). Install it
through the repository's marketplace: `openclaw plugins install git:…` does not work, because
that route takes native OpenClaw plugins only and Stockwatcher is a skill bundle.

```bash
openclaw plugins install stockwatcher --marketplace https://github.com/ktoetotam/stockwatcher-plugin --accept-capabilities
```

To get a newer version later:

```bash
openclaw plugins update stockwatcher --accept-capabilities
```

Then ask, for example, "show me the S&P 500" or "this is my portfolio: 10 AAPL, 5 MSFT".

## Layout

- `.claude-plugin/plugin.json` and `.claude-plugin/marketplace.json` — the Claude Code
  plugin, and what lets this repository be added as a marketplace there.
- `.codex-plugin/plugin.json` and `.agents/plugins/marketplace.json` — the same for Codex.
- `plugin.json` — the portable manifest (Agent Plugins format) for other apps that read it.
- `assets/logo.svg` — the icon shown in Codex's plugin list.
- `skills/stockwatcher/` — the skill: `SKILL.md`, the dashboard page, the server and
  command scripts, and the shipped data (stock list, index members, themes).

The scripts that refresh the shipped data are kept separately and are not part of this
repository.

## What stays on your computer, and what it contacts

Your portfolios, remembered research and the count of what you ask for are kept in one file
on your computer and are never sent anywhere. The dashboard can be opened only from your
own computer; other websites cannot read it.

The skill contacts these services, with no account and nothing about you:

- Yahoo Finance and Nasdaq for prices and the stock list;
- SEC EDGAR and OpenFIGI when you ask for an investor's portfolio;
- ApeWisdom when you ask about r/wallstreetbets;
- airealist.org, at most once a day while the dashboard is in use, for the maker's current
  workshop dates. The page shows one small line about one of them or the newsletter; the
  "×" next to it hides it for a week.
