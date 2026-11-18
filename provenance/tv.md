# Sony TV codes: provenance

New codes proposed for infrared-protocols, on top of the 40 `SonyTVCode`
entries PR #134 added. PR #134 asked for at least three source remotes per
code.

Sources checked:

- **IRCC**: Sony's IRCC table for Bravia displays (pro-bravia.sony.net,
  "IRCC-IP"). It's the same data sets report over `getRemoteControllerInfo`.
- **IRDB**: probonopd/irdb, `codes/Sony/TV/` (`1,-1`, `26,-1`, `151,-1`).
- **LIRC**: lirc-remotes, `remotes/sony/`.
- **pybravia**: `CODE_POWER_ON` in pybravia's `const.py` (used by core's
  braviatv integration).

| Code | Address / bits | Command | Sources |
| --- | --- | --- | --- |
| POWER_ON | 0x01 / 5 | 0x2E | IRDB, LIRC RM-Y103, pybravia |
| POWER_OFF | 0x01 / 5 | 0x2F | IRDB, LIRC RM-Y103 |
| HDMI_1 to HDMI_4 | 0x1A / 8 | 0x5A to 0x5D | IRCC, IRDB |
| PLAY | 0x97 / 8 | 0x1A | IRCC, IRDB, LIRC RM-ED035, RM-YD010 |
| PAUSE | 0x97 / 8 | 0x19 | IRCC, IRDB, LIRC RM-YD010 |
| STOP | 0x97 / 8 | 0x18 | IRCC, IRDB, LIRC RM-ED035, RM-YD010 |
| REWIND | 0x97 / 8 | 0x1B | IRDB, LIRC RM-ED035, RM-YD010 |
| FAST_FORWARD | 0x97 / 8 | 0x1C | IRDB, LIRC RM-ED035, RM-YD010 |
| PREVIOUS | 0x97 / 8 | 0x3C | IRCC, IRDB, LIRC RM-ED035, RM-YD010 |
| NEXT | 0x97 / 8 | 0x3D | IRCC, IRDB, LIRC RM-ED035, RM-YD010 |

Gaps: POWER_OFF and HDMI 1 to 4 have two independent sources. Testing them
on your own sets and naming the models in the PR is the best way to fill
that in.
