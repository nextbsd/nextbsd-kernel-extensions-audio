# nextbsd-kernel-extensions-audio

Audio kernel extensions for NextBSD: drivers for modern laptop audio that the
FreeBSD-derived `snd_hda` driver cannot reach. These ship as kext bundles in
`/System/Library/Extensions`, like the drivers in
[nextbsd-kernel-extensions](https://github.com/nextbsd/nextbsd-kernel-extensions)
and [nextbsd-kernel-extensions-graphics](https://github.com/nextbsd/nextbsd-kernel-extensions-graphics).

The first target is **Intel Sound Open Firmware (SOF) with SoundWire codecs**: the
audio DSP in Intel laptops from Tiger Lake on, with speakers and microphones on a
SoundWire bus instead of an HDA codec. The first machine is the Dell XPS 13 9320
(Alder Lake, SKU 0AF3: two Realtek RT1316 amplifiers on SoundWire links 1 and 2,
a Realtek RT714 microphone codec on link 0, no headphone jack). Without these
drivers, NextBSD finds the HDA controller and no sound device.

Plan and design: [the wiki](https://github.com/nextbsd/nextbsd-kernel-extensions-audio/wiki).

## Licensing

- **This repository is BSD-2-Clause** (see [LICENSE](LICENSE)). New code written
  for NextBSD carries that licence and Joseph Maloney's copyright.
- **Code derived from Linux files that are dual-licensed `GPL-2.0-only OR
  BSD-3-Clause`** (most of the Linux SOF driver and SoundWire bus, copyright Intel
  Corporation and others) is used under its **BSD-3-Clause** option. Such files keep
  their original copyright notices and licence text, add a line saying they were
  modified for NextBSD, and carry an SPDX identifier saying which licence applies.
- **No code from GPL-only Linux files** (for example the `sof_sdw` machine driver,
  `sound/soc/sdw_utils`, the Realtek SoundWire codec drivers, or the ASoC core). They
  may be read as a reference for hardware behaviour, but what lands here is written
  for NextBSD.
- **Firmware and topology files** are not our code. They live under `firmware/`, each
  vendor's next to its own licence (see [firmware/README.md](firmware/README.md)).

The SOF maintainers made the SOF drivers permissive on purpose, to allow ports
like this one ([thesofproject discussion #9506](https://github.com/orgs/thesofproject/discussions/9506)).
