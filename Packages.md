# Packages

Note that packages included in the default OpenWRT configuration, like `dropbear`, are not included in this list regardless of their necessity.

## Required

### Mesh capability

`alfred`, `batctl-full`, `kmod-batman-adv`, `wpad-wolfssl`:

These are the bare minimum technical requirements for a node to mesh. It's possible to replace `wpad-wolfssl` with `wpad-mesh-wolfssl` to save ~100KB, but that shouldn't be necessary except under the most desperate circumstances.

### Routing

`bmx7-uci-config`, `kmod-bmx7`, `luci-app-bmx7`:

These are not strictly necessary for a working mesh, but are likely to be more flexible and reliable than built-in routing, and eliminate dependence on batadv gw_mode.

## Recommended

### Internationalization

`luci-i18n-en`, `luci-i18n-es`, `luci-i18n-fr`, `kmod-nls-cp437`, `kmod-nls-iso8859-1`, `kmod-nls-utf8`:

These can also be installed on a case-by-case basis, but are important in our goal of empowering people to support their own devices, and English, Spanish, and French seem likely to meet most users' needs. `kmod-nls` modules are much less likely to be technically necessary, but are also extremely small.

### USB storage support

`kmod-usb-storage`, `kmod-usb2`, `kmod-usb3`, `kmod-fs-ext4`, `e2fsprogs`, `block-mount`:

These are necessary (with the possible exception of `kmod-usb3`) for USB storage support, which is useful for e.g. file transfer, and probably merit being installed on any devices with a USB port. Also helpful, but less important, are `blockd` for automounting and `usbutils` for diagnostics.

## For hub use

### Traffic security

`kmod-wireguard`, `luci-app-wireguard`, `wireguard-tools`:

These allow us to route traffic through a VPN, which should be considered necessary for all mesh 'exit' nodes. `openvpn-wolfssl` and `luci-app-openvpn` are also available for this purpose, but WireGuard seems to be generally better software at this point.

`tor`:

Because access to the Tor network is, unlike most VPN services, freely available, it can be used as an alternative or in conjunction with VPNs for exit node traffic security.

### Traffic shaping

`sqm`, `sqm-scripts-extra`, `luci-app-sqm`:

These allow us to implement bandwidth limits, among other QoS features, and should probably be installed on all exit nodes.

### Traffic/device monitoring

`vnstat2`, `luci-app-vnstat`:

These allow us to monitor traffic to identify potential configuration issues, misused or compromised devices, etc. `collectd` and `luci-app-statistics` are other possibilities for this role.

`openwisp-config`, `openwisp-monitoring`, `luci-app-openwisp`:

OpenWISP is a larger-scale framework for network management that may be useful for pushing firmware updates or configuration changes.

`watchcat`, `luci-app-watchcat`:

Watchcat is a ping-based network watchdog that may be useful for automatically identifying and fixing network failures.

## Optional

### Ad blocking

`adblock`, `luci-app-adblock`:

These allow for more traditional advertisement and malware blocking, but can also be used to disable tracking pixels, cookies, etc.

### Captive portal software

`opennds`:

Though there was general agreement that an always-on captive portal was not a good choice, having the software available might facilitate occasional communication to users about network issues, etc. when needed.

### Other software

`nano-full`:

please don't make me learn vim