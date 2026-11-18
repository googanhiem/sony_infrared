# Sony AV receiver codes: provenance

Codes from ha-sony-receiver-ir, checked for an infrared-protocols PR. Sony
AV receivers (STR-DH, STR-DN, STR-DG, STR-DA, ...) use 15-bit SIRC on two
addresses: 0x30 for amplifier keys and 0xB0 for sound field and menu keys.
None of these are in infrared-protocols yet.

Sources checked:

- **IRDB**: probonopd/irdb, `codes/Sony/Receiver/` (`48,-1` is 0x30,
  `176,-1` is 0xB0). It lists one name per key, not per remote.
- **LIRC**: lirc-remotes, `remotes/sony/`. Remotes that matched: RM-AAU014,
  RM-PP411, RM-PP860, RM-U306A and `av-system2`.

The IRDB column gives the name IRDB uses, and the LIRC column counts matching
remotes.

| Code (ha-sony-receiver-ir) | Address | Command | IRDB name | LIRC |
| --- | --- | --- | --- | --- |
| POWER | 0x30 | 0x15 | POWER | 4 |
| POWER_ON | 0x30 | 0x2E | POWER ON | 0 |
| POWER_OFF | 0x30 | 0x2F | POWER OFF | 0 |
| SLEEP | 0x30 | 0x60 | SLEEP | 2 |
| VOLUME_UP | 0x30 | 0x12 | VOLUME UP | 4 |
| VOLUME_DOWN | 0x30 | 0x13 | VOLUME DOWN | 4 |
| MUTE | 0x30 | 0x14 | MUTE | 3 |
| BD_DVD | 0x30 | 0x7D | DVD | 3 |
| GAME | 0x30 | 0x1E | VIDEO2 | 4 |
| SAT_CATV | 0xB0 | 0x03 | (none) | 1 |
| VIDEO | 0x30 | 0x22 | VIDEO1 | 3 |
| VIDEO_3 | 0x30 | 0x42 | VIDEO3 | 2 |
| TV | 0x30 | 0x6A | TV/SAT | 2 |
| SA_CD_CD | 0x30 | 0x25 | CD/SACD | 3 |
| TUNER | 0x30 | 0x21 | TUNER | 4 |
| PRESET_UP | 0x30 | 0x10 | PRESET UP | 0 |
| PRESET_DOWN | 0x30 | 0x11 | PRESET DOWN | 0 |
| NUM_1 to NUM_4 | 0x30 | 0x00 to 0x03 | 1 to 4 | 2 |
| NUM_5 to NUM_0 | 0x30 | 0x04 to 0x09 | 5 to 0 | 1 |
| TWO_CH | 0xB0 | 0x41 | 2 CH | 4 |
| AFD | 0xB0 | 0x42 | AFD | 2 |
| MOVIE | 0xB0 | 0x43 | MOVIE | 2 |
| MUSIC | 0xB0 | 0x49 | MUSIC | 2 |
| AMP_MENU | 0xB0 | 0x77 | (none) | 4 |
| NAV_UP / DOWN / LEFT / RIGHT | 0xB0 | 0x78 to 0x7B | (none) | 1 |
| DISPLAY | 0x30 | 0x4B | (none) | 1 |
| TEST_TONE | 0xB0 | 0x4A | TEST TONE | 2 |

Strong (3 or more sources): power, volume, mute, DVD, VIDEO 1, VIDEO 2,
CD/SACD, tuner, 2CH, sleep, VIDEO 3, TV/SAT, AFD, movie, music, test tone,
digits 1 to 4, and amp menu (4 LIRC remotes, no IRDB entry).

Weak (2 or fewer sources): discrete power on/off, preset up/down, digits 5
to 0, SAT, the menu arrows and display. These need your own captures, or
should wait.

Naming: ha-sony-receiver-ir uses the labels on newer remotes (BD/DVD, GAME,
SAT/CATV, VIDEO) and assumes they reuse the codes of the inputs they
replaced. Every source names them DVD, VIDEO 2, SAT and VIDEO 1. The library
should use the source names, and the integration can show friendlier labels.
