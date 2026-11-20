# Pi deployment scope

The source targets the existing CRANIUM setup: Pi 4, ARM64 Debian 12 Bookworm,
800 x 480 DSI display, Sway/Wayland session, USB mounting helpers and a pi user.
The existing offline installer assumes this prepared environment. It is not a
fresh-OS bootstrapper. Preserve the Pi's own Mesa, Wayland and C/C++ runtime.

Build and test the staged app first using the root README. For a first partner
test, run the staged app from its existing directory inside a graphical session
with an isolated profile. Confirm screen orientation, touch, USB browsing,
FLX4 MIDI, audio routing, headphone cue and two-deck playback before deployment.

For the existing CRANIUM appliance, create the offline bundle using bundle-pi.py.
Copy these helper files from cranium-nauticmixxx/cranium/pi/ alongside the bundle's
manifest.json and nauticmixxx-arm64-bookworm.tar.gz:

```text
installer.py  install.sh  launch.py  app-menu.sh
session.py    kiosk.py    diag.py    start.png
```

Inspect the installer before running it. The installer updates /opt/cranium and
the appliance session; it keeps backups and preserves existing profile/audio
settings. Do not run the boot-partition install.sh manually on a new system.
For an on-device update of the existing appliance with no pending boot installer,
use sudo python3 /path/to/bundle/installer.py, then restart the application/session.
It is an explicit deployment action, not a build/test step.

The older Mac SD-card staging helper is retained for the prepared appliance only.
It now requires --boot-volume, --expected-volume-uuid and
--expected-root-partuuid instead of containing the original owner's device IDs.
It still checks for the original appliance's completed installation and compatible
boot layout. It refuses mismatches; do not weaken those checks to force another
SD card through it. No SD card is written by cloning, host checks or building.
