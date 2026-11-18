# sony_infrared

Staging for a `sony_infrared` integration in Home Assistant core: one
integration for Sony TVs and Sony AV receivers controlled over infrared. It
replaces two custom integrations:

- [ha-sony-bravia-ir](https://github.com/googanhiem/ha-sony-bravia-ir) (TVs)
- [ha-sony-receiver-ir](https://github.com/googanhiem/ha-sony-receiver-ir) (receivers)

This repo isn't installable. It holds the patches, docs drafts and code
provenance, so each PR can be reviewed and opened by hand.

## Layout

- `core/`: patches for home-assistant/core, one per PR, applied in order.
- `infrared-protocols/`: patches for home-assistant-libs/infrared-protocols.
- `docs/`: the home-assistant.io page, kept in step with the core PRs.
- `provenance/`: where each new IR code comes from.

## Plan

| # | Repo | PR | Needs | Status |
| --- | --- | --- | --- | --- |
| C1 | core | Add Sony Infrared integration: TV device type, media player (power toggle, volume, mute, channel) | infrared-protocols 10.7.0 (already in core) | Open: home-assistant/core#193272 (patches 0001 and 0002, a review fix) |
| L1 | infrared-protocols | Discrete power, HDMI 1 to 4 and playback codes for Sony TVs | Draft of C2 | Patch ready |
| C2 | core | TV: discrete power, source select, play/pause/stop, assumed state restored on restart | L1 released and the core bump | Todo (port from ha-sony-bravia-ir) |
| L2 | infrared-protocols | Sony AV receiver codes | Draft of C3 | Todo |
| C3 | core | Receiver device type (media player) | L2 released | Todo |
| C4 | core | Button platform | C2, C3 | Todo |
| C5 | core | Event platform (remote key presses) | C4 | Todo |
| C6 | core | Track physical remote (options flow) | C5 | Todo |
| C7 | core | Diagnostics and reconfigure flow (Gold) | | Todo |
| C8 | core | Strict typing (Platinum) | | Todo |

The library PR template requires a linked draft core PR, and core can only
pin a released library version. So for L1: open C2 as a draft, open L1 linking
it, and once L1 is released, bump `infrared-protocols` in
`homeassistant/components/infrared/manifest.json` (core wants that bump as its
own PR) before marking C2 ready for review.

## Applying the patches

core (patches are made against `dev` at fc0b2fc5):

```bash
git checkout -b sony_infrared upstream/dev
```

```bash
git am /path/to/sony_infrared/core/*.patch
```

infrared-protocols (made against `main` at f160043):

```bash
git checkout -b sony-tv-extended-codes origin/main
```

```bash
git am /path/to/sony_infrared/infrared-protocols/0001-*.patch
```

## Checks run on C1

- 15 tests pass, with 100% coverage of the integration.
- All of core's pre-commit hooks pass: ruff, prettier, mypy, pylint and
  hassfest, with hassfest validating Bronze.
