# Local Image Build Guide

This fork (`Agent-Mouses/agent-broker`) tracks upstream `openabdev/openab` with custom patches on the `custom` branch.

## Branches

- `main` — mirrors upstream `openabdev/openab` exactly
- `custom` — our patches rebased on top of main (used to build local Docker images)

## Build Local Image

```bash
git clone https://github.com/Agent-Mouses/agent-broker.git
cd agent-broker
git checkout custom
docker build -t agent-broker-configured:latest .
```

## Update to New Upstream Version

```bash
cd agent-broker
git fetch upstream
git checkout main
git merge upstream/main
git push origin main

git checkout custom
git rebase main
# resolve conflicts if any
git push origin custom --force-with-lease

# rebuild image
docker build -t agent-broker-configured:latest .
```

## Current Patches (on `custom` branch)

- `allow_bot_messages` config option — when `true` in `[discord]`, the bot processes messages from other bots (e.g. other agent-broker instances in the same channel). Defaults to `false`.
