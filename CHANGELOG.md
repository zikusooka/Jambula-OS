# Changes

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
