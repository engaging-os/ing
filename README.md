# ing

**Engaging OS from the command line.**

`ing` lets scripts, scheduled jobs, and AI agents work with an organization running [Engaging OS](https://engaging.net)—not only viewing but also doing. It connects to the same server that AI apps like Claude and ChatGPT use. It signs in the same way, and it can reach only what your roles in that organization allow.

This repository holds release downloads only.

## Install

macOS and Linux:

```sh
curl -fsSL https://github.com/engaging-os/ing/releases/latest/download/install.sh | sh
```

The script picks the right build for your machine, checks it against the release's checksums, and installs it to `~/.local/bin`. Run it again to update.

Windows: download `ing-windows-x64.exe` from the [latest release](https://github.com/engaging-os/ing/releases/latest).

Each download is a single self-contained file, with nothing else to install.

## Get started

Sign in to your organization's site. Your browser opens its sign-in page:

```sh
ing login https://your-organization.example
```

Then:

```sh
ing whoami                   # who you are, and your roles
ing read engaging://awaiting # what needs your attention
ing tools                    # everything you can do, with descriptions
```

## With an AI agent

Coding agents such as Claude Code and Codex can use `ing` without any setup: they learn it from `ing --help` and `ing tools`. Once you've signed in, try asking one to "use ing to show me what's awaiting me."

`ing instructions` prints the guidance the site gives agents, which makes it a good first command for one.

## Commands

| Command | What it does |
| --- | --- |
| `ing login <site>` | Sign in through the site's consent page |
| `ing logout` | End the connection |
| `ing status` | Sites you're signed in to |
| `ing use <site>` | Choose the default site |
| `ing instructions` | The site's guidance for agents |
| `ing whoami` | Your user, roles, and the site's prompts |
| `ing tools` | Available tools, with descriptions and input schemas |
| `ing call <tool> --arg value …` | Call a tool |
| `ing read <engaging://uri>` | Read a resource |

For example:

```sh
ing call ing_query_console --as principal@lincoln-high --console_id 12 --mode search --search Tampa
echo '{"Title": "New"}' | ing call ing_perform_operation --as principal@lincoln-high \
  --action create --collection Staff --data -
```

`--as position@body` says which of your roles you're acting in. `--json` passes all arguments at once, and `@file` or `-` reads a value from a file or standard input.

Results go to standard output as JSON. Messages go to standard error. Exit codes: `0` success, `1` the site or tool reported an error, `2` usage, `3` sign in again.

## Signing in on a machine without a browser

Over SSH, or on a server, run `ing login <site> --no-browser`. Open the printed address on any device, sign in, and paste the address the browser ends up on—it won't load—back into the terminal.

## Security

- `ing` never sees your password. You type it into your organization's own site, which gives `ing` its own connection.
- Every request is checked against your roles, just as on the website.
- A connection lasts up to 30 days. It's listed as "Engaging CLI" under **My Profile → Connect AI** on the site, where you can end it at any time; `ing logout` ends it too.
- Credentials are stored in `~/.config/engaging/credentials.json`, readable only by you.

## About Engaging OS

Engaging OS is an operations platform for organizations, made by [Engaging](https://engaging.net). Ask your organization's administrator whether its site offers AI connections.
