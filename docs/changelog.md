# Changelog

All notable changes to SharKNX are documented in this file.

---

## [1.3.2+19] - 2026-01-28

### Added
- **DPT 250.600 Support** - New widget for relative brightness & color temperature control with step-based adjustments (-7 to +7)
- **Visual Feedback for Quick Send** - Command chips now show loading spinner, success (green), or error (red) states with 300ms cooldown

### Improved
- **Quick Send Enhancements** - Drawer stays open after sending, increased history from 3 to 10 commands, added read commands with blue badge indicator
- **Badge Layout** - Status badges now use horizontal scroll to prevent wrapping and clipping, improved spacing and shadow rendering
- **Snackbar Appearance** - Slimmer height, proper floating with 8px bottom margin, removed shadow for cleaner look
- **Connection UI** - Connect button now shows loading state during gateway connection

### Fixed
- **Floating Snackbar Positioning** - Snackbars now automatically position above FABs and bottom bars without manual offset calculation
- **Gateway Badge Visibility** - Added visual disabled state (50% opacity) when no gateway is selected
- **Badge Shadows** - Fixed shadow clipping issues in release builds
- **Read Command Handling** - Fixed Quick Send to properly call sendRead() instead of always using sendWrite()

## [1.3.1+18] - 2026-01-27

### Improved
- **Connection Feedback** - Connect button now displays loading state during gateway connection for better user feedback

## [1.2.0+17] - 2026-01-23

### Improved
- **Secure Connections** - Improved stability in KNX IP Secure connections

### Fixed
- **DPT 3.008 Widget** - Fixed blind control slider value jumping issue

## [1.2.0+16] - 2026-01-23

### Improved
- **Secure TCP Connections** - Improved stability in Secure TCP connections
- **Multi-Slot Support** - Optimized multi-slot connection with lazy key derivation and automatic filtering across all slots

## [1.2.0+15] - 2026-01-18

### Added
- **Shark Hunt Pages** - Create custom pages with quick send actions for KNX commands and complex monitor filters for advanced diagnostics
- **Full Feature Release** - Initial release with core KNX monitoring and diagnostics capabilities

### Improved
- **Gateway Discovery** - Enhanced stability and reliability of the gateway discovery function

### Fixed
- **Telegram Decoding** - Resolved issues in telegram decoding for improved data accuracy
- **DPT Handling** - Fixed various data type encoding/decoding issues
