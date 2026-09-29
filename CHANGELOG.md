# Changes

## 2026.9.0

### Added
- Add initial support for x86_64
- Add initial support for Raspberry Pi Zero W v1.1
- Add ZeroPlay package and enable it along with libwebsockets on Raspberry Pi Zero W
- Add zeroplay-remote service for remote-controlled playback from any web browser on PC or mobile
- Add PipeWire support to the ZeroPlay service
- Add jambula-radio-volume service for time-based speaker volume control
- Add open gate audio alert handling to the MQTT events listener
- Add initial support for NFS file sharing on clients
- Add AdGuard Home ad blocker support with a buildroot package and setup option
- Add AdGuard DNS redirect and DoT block to the jambula-internal firewall zone
- Add WLAN_INTERFACE variable to global functions
- Add support for colors in dialog menus
- Show device name alongside MAC address in the Bluetooth discovery list
- Save errors to a log file during jambula-setup without breaking dialog screens

### Changed
- Bump Frigate to version 0.17.2 (via 0.17.1)
- Use a dedicated interface name (ap0) for the hostapd AP instead of the shared wlan device, and add it to the internal firewall zone
- Move detection and selection of wireless device(s) in setup scripts to a unified global function
- Refactor initial boot script for configuring system services
- Move systemd service disabling from the initial boot script to pre-configured presets
- Move psplash progress reporting from the jambula-initial-boot service into the called configuration scripts
- Start dnsmasq manually during prosody setup instead of via systemd
- Migrate tvheadend system user and config path from hts to tvheadend to match the buildroot package user
- Improve Bluetooth device auto-reconnection reliability during boot
- Update Jambula radio streams, schedule and speaker volume
- Update default motion configuration file
- Suppress verbose output during boot on Raspberry Pi Zero W
- Remove obsolete Raspberry Pi 1 Model B kernel config
- Remove realtek kernel module from the automatic startup list
- Skip snapcast client setup prompts when the system role is already known
- Switch system role and internet connection type dialogs from checklist to radiolist in jambula-setup
- Adjust jambula-setup dialog height for the selected options list
- Fix HTTP casing in the nginx setup dialog message
- Make dialog menu wording in select_wifi_device generic to cover both server and client setups
- Clarify pairing prerequisites and connection requirements in the Bluetooth setup script
- Remove redundant dialog clear at the end of the Tailscale setup script
- Remove leftover debugging code from the wifi client setup script
- Revert logging and descriptor redirection in functions introduced in dcdff7a (did not work as intended)
- Revert jambula-setup logging rules inside bash_profile to the original

### Fixed

#### Audio and Bluetooth
- Route audio playback through PipeWire so output to Bluetooth devices works
- Enable onboard Bluetooth on Pi Zero W by removing the disable-bt overlay and freeing the UART console
- Increment psplash progress after configuring wireplumber bluez during initial setup
- Resolve missing ALSA UCM configuration errors by creating a dummy ucm.conf
- Remove unsupported metadata_selector option from MPD input config
- Create the mpd log file and update its group ownership in the mpd server and playlists setup script
- Update snapclient systemd unit with dependencies and delay to resolve connection refused error during boot
- Remove unused START_SNAPCLIENT variable from the snapclient setup script

#### Networking, Wi-Fi and hotspot
- Configure the wifi interface via systemd-networkd during the temporary hotspot so the kea DHCP server works
- Restart kea-dhcp4 after hostapd on wifi band switch to restore client connectivity
- Enable kea DHCP lease persistence and remove the backup .orig config file
- Mask systemd-networkd-wait-online.service to reduce boot time
- Initialize Wi-Fi mode before checking the access point band in jambula-switch-wifi-ap-band
- Fall back to hostapd_cli for WiFi band when iw reports no channel
- Disable the in-kernel rtl8xxxu module to prevent conflict with the out-of-tree rtl8188eu AP driver
- Resolve hostapd startup errors by disabling 802.11ac on the 2.4 GHz AP and using the US regulatory domain for the temporary setup hotspot
- Harden initial temporary wifi hotspot setup script logic, fix kea syntax, and remove .local from avahi configuration
- Remove .local TLD from avahi static hosts configuration to prevent mDNS hostname conflicts
- Run dnsmasq in foreground and wait for the br0 WiFi hotspot IP to prevent systemd SIGTERM
- Silence firewall-cmd output during hostapd internal zone assignment
- Ensure AP networking is set up before configuring other services
- Check that the AP bridge device file exists before reading it to avoid initial setup errors
- Update and resolve bugs in wifi client setup
- Use WLAN_INTERFACE as the default wifi device in the prosody setup script
- Use WLAN_INTERFACE as the default wifi device in the AP networking setup script
- Restart service always when setting up Tailscale remote access
- Update ntp setup script to overwrite timesyncd config with local and remote NTP pool servers
- Increase fs.inotify.max_user_watches to prevent systemctl failures

#### Boot and initial setup
- Resolve initial boot hangs and delays while configuring the temporary hotspot
- Reduce initial boot delays in temporary Wi-Fi AP setup by replacing a blocking avahi poll with a bounded wait and trimming sleep times
- Reduce initial boot delays in system services setup by separating disable from stop and only stopping running units
- Increase jambula-initial-boot timeout to 300s to prevent premature termination
- Update initial-boot systemd service ordering and add error handling for psplash calls
- Add dhcpcd to the disable list, prevent abort on disable failure, and disable all matching unit extensions per service
- Add frigate, mariadb and radicale services to the systemd disable list during initial system configuration
- Correct zram-swap.service ordering to break a sysinit dependency cycle during boot
- Disable jambula-radio-volume.timer by default to stop repeated failures from missing config on first boot
- Stagger jambula systemd timers and remove RandomizedDelaySec to prevent concurrent execution
- Delay tty getty startup to keep boot log noise off the login prompt
- Clear invalid getty credential import path caused by slashes in instance names
- Display only one logo at boot time
- Resolve missing polkit rules directory errors via tmpfiles configuration
- Add clock system group to buildroot users_table.txt
- Write system time to RTC on sync to prevent hardware drift during jambula-clock execution
- Ensure the jambula config directory exists and prevent duplicate systemd symlink creation during smart radio setup
- Update setup script to read a single selection from radiolist dialog menus

#### Raspberry Pi Zero W hardware
- Reduce CMA reservation to 128MB to free up RAM
- Unblacklist bcm2835_codec for hardware H.264 decode and drop the redundant modules-load.d entry
- Enable bcm2835_codec module autoload during boot
- Increase GPU memory and enable the KMS driver for video playback
- Remove cgroup memory tracking from the kernel command line
- Enable dwc2 host mode overlay for USB keyboard/device support
- Trim linux-systemd.fragment to reduce cgroup/audit stack pressure, remove stray ARM64 4K-page fragment, and prune unused RPi board config/readme variants for raspberrypi-0-w

#### Services and packages
- Rework rain phrasing and make heavy-rain warnings list every forecasted day/period in the jambula-weather tool
- Improve MySQL database setup with startup ping checks, waits and an auto-reinitialization fallback
- Wait for the prosody systemd service to be active before adding chat users
- Update and rename patch to allow prosody to build with Lua 5.4
- Source the functions file in the tvheadend setup script to fix a missing dialog command
- Update tvheadend systemd service user to match the buildroot package
- Update frigate web symlink to the dist folder to fix frontend camera display
- Remove premature frigate web directory creation in the buildroot package makefile that prevented the symlink from being placed correctly
- Generate frigate sysconfig dynamically using buildroot package makefile variables
- Include the frigate web symlink in the frigate uninstallation script
- Remove legacy kodi reference from raspberrypi_5 defconfig paths

### Build
- Update buildroot config for Raspberry Pi Zero W (multiple updates)
- Update buildroot config for Raspberry Pi 1 B
- Update default config and variant fragments to match latest sources plus Linux kernel and headers
- Remove legacy options from config files in the latest sources
- Remove rpi4 firmware, bind, ntpd, squid and nut packages from buildroot config files for rpi5
- Increase TARGET_ROOTFS_EXT2_SIZE for all rpi5 images (7680M, then 7936M)
- Update BR2_LINUX_KERNEL_PATCH path in buildroot configs for rpi5
- Add rp1-pio kernel config fragment for Raspberry Pi 5 to fix rp1-pio probe error -2
- Add simple free and paid build targets to automate setup, configs and patches
- Improve package patching logic and strip level in the pre-build script
- Add rsync patch to fix compilation failure during package build
- Fix clean build failures of the pydio-cells package by adding missing dependencies and correcting directory permissions
- Add site-packages and working dir to PYTHONPATH in frigate package sysconfig generation
- Replace boot logo image assets with updated designs
- Remove the time command from free and paid image compilation steps


## 2026.5.3

### Added
- Add openNDS captive portal setup script
- Add system user definition for the openNDS captive portal server
- Integrate openNDS captive portal web pages into the post-build sync pipeline
- Add company domain name variable in global functions

### Changed
- Migrate AP wireless and routing services from wlan0 to the br0 bridge
- Refactor opennds setup script to use native configuration rules
- Use default and auto-generated database credentials for Pydio Cells setup
- Display created access credentials in MySQL database setup
- Secure password creation in the prosody setup script
- Refresh initial setup wizard layout and text colors for an improved onboarding experience
- Polish root password update dialog wording in jambula-setup
- Log jambula-setup background errors to keep screens clean
- Simplify systemctl reboot command during initial setup and protect the setup log variable called by other scripts
- Suppress background networking errors during the initial setup wizard

### Fixed
- Remove duplicate hardcoded wlan1 reference in internet via wpa_supplicant setup
- Ensure the MPD data directory and database exist during setup
- Evaluate wifi mode correctly in jambula-sysinfo
- Add missing http protocol prefix to the completion notice in webcam setup

### Build
- Upgrade openNDS package to version 11.0.0
- Add dnsmasq.conf to the overlay directory to fix a missing file error during initial setup
- Add kea DHCP lease parsing and fix dnsmasq systemctl reload in opennds libraries
- Add rpi5 Broadcom firmware to the rootfs overlay to ensure hostapd stability


## 2026.5.2

### Security
- Enable Yama LSM for ptrace restriction to mitigate CVE-2026-46333
- Disable vulnerable ESP and RXRPC modules to mitigate CVE-2026-43284

### Changed
- Update Bluetooth setup instructions to use the generic default audio sink
- Refine MySQL service startup dialog during initial database setup
- Polish MPD setup prompts and titles
- Improve root password prompt dialog during initial setup

### Fixed
- Route kea-dhcp clients to the gateway for local domain resolution
- Trim whitespace from vendor description and modernise bash test syntax in hostapd setup
- Include Chat Server in the setup options file during initial configuration
- Update sysinfo display to show edition instead of install date
- Simplify and fix network gateway IP and device parsing logic
- Ensure the options file is freshly created during setup
- Enable snapclient without starting it during initial setup to prevent shutdown hang
- Suppress journal log spam and correct mpc status parsing
- Ignore commented variant entries when parsing the os-release file in project functions


𝟐𝟎𝟐6.5.1
--------

Added XMPP chat server (Prosody) to the additional setup options.

Added Subject Alternative Name (SAN) support to the SSL certificate generation script.

Replaced systemd-resolved stub with dnsmasq for local DNS and changed the default system domain suffix to .lan.

Mitigated CVE-2026-31431 local privilege escalation vulnerability in the kernel.

Resolved critical system hangs during shutdown and reboots following the initial first-boot setup.

Forced hard reboots via kernel mode to ensure a pristine cold-boot state after setup.

Resolved a psplash boot hang caused by a missing framebuffer device, and removed the duplicate xlogo boot logo.

Implemented stalled playback detection and recovery for online streams in MPD.

Increased the TARGET_ROOTFS_EXT2_SIZE to 7168M for default and community editions.

Added Raspberry Pi 5 WiFi firmware symlinks to resolve boot errors.


𝟐𝟎𝟐6.5.𝟎
--------

Protect against the Copy Fail vulnerability

Added support for 5 GHz Wi-Fi band with reduced Bluetooth interference on combo wireless devices

Introduced built-in Prosody (XMPP) server with setup scripts and DNS support for local, offline messaging

Added new tool: jambula-switch-wifi-ap-band for easier Wi-Fi band management

Enabled automatic Wi-Fi interface detection during hotspot and client setup

Improved firewall configuration with updated zones, policies, and service rules (including XMPP and OpenNDS)

Added OpenNDS captive portal support with nginx integration

Added SSL certificate setup script

Upgraded Frigate to 0.17.x with continuous recording support and improved setup

Upgraded go2rtc to 1.9.14 with improved camera configuration

Enhanced MQTT tooling with multi-topic support and motion alerts

Fixed slow shutdown issues by improving service ordering (snapclient)

Added watchdog to improve MPD service reliability

Improved dnsmasq with nftables (nftsets) support

Added WebDAV support via nginx module

Cleaned up deprecated patches and removed unused packages

General system improvements, bug fixes, and stability enhancements


𝟐𝟎𝟐𝟓.𝟗.𝟎
---------

𝐁𝐥𝐮𝐞𝐭𝐨𝐨𝐭𝐡 𝐬𝐩𝐞𝐚𝐤𝐞𝐫 𝐬𝐮𝐩𝐩𝐨𝐫𝐭: Added support for Bluetooth audio devices which is ideal for voice prompts or music output.

𝐒𝐰𝐢𝐭𝐜𝐡𝐞𝐝 𝐭𝐨 𝐊𝐞𝐚 𝐃𝐇𝐂𝐏: Replaced dnsmasq with 𝐊𝐞𝐚 𝐃𝐇𝐂𝐏 for better dynamic addressing management.

𝐖𝐢𝐅𝐢 𝐡𝐨𝐭𝐬𝐩𝐨𝐭 𝐜𝐥𝐢𝐞𝐧𝐭 𝐜𝐨𝐮𝐧𝐭 𝐢𝐧 𝐌𝐎𝐓𝐃: See how many clients are connected to your hotspot right in the system’s MOTD.

𝐐𝐑 𝐜𝐨𝐝𝐞 𝐨𝐧 𝐢𝐧𝐢𝐭𝐢𝐚𝐥 𝐥𝐨𝐠𝐢𝐧: Displays a QR code linking to vendor/device info, useful for branding or support.

𝐈𝐦𝐩𝐫𝐨𝐯𝐞𝐝 𝐬𝐞𝐭𝐮𝐩 𝐭𝐨𝐨𝐥𝐬: Smoother first-time setup experience with updated scripts.

𝐇𝐨𝐦𝐞 𝐀𝐬𝐬𝐢𝐬𝐭𝐚𝐧𝐭 𝐮𝐩𝐝𝐚𝐭𝐞𝐝: Latest Home Assistant version included to keep your platform up to date.

𝐁𝐮𝐠 𝐟𝐢𝐱𝐞𝐬: Minor fixes including firewall and weather integration improvements.
