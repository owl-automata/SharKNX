# Changelog

All notable changes to SharKNX are documented in this file.

## Known Limitations

iOS Version: Multicast Discovery and Conmmand Send does not work. Will be available on next release version, planned for end of February 2026.

## [1.6.3+27] - 2026-02-17

### Improved
- **Project Page View** - Persistent section expanded state across tab changes.

---

## [1.6.2+24] - 2026-02-16

### Fixed
- **Command Composer State** - Fixed DPT value encoding errors when opening command composer from group address detail sheet. Value field now properly initializes with DPT-specific defaults (e.g., "0.0" for DPT 9.x) when DPT is provided without explicit value, eliminating "failed to encode value off" errors.
- **Connection Timeout Settings** - Fixed slider crash when loading saved timeout values outside new range. Adjusted connection timeout range from 5-30s to 1-10s with 3s default (was 10s) for faster connection attempts. Added value clamping during settings load to handle legacy saved values.

### Improved
- **Auto-Connect Feature** - Read/Write buttons in GA detail sheet, Telegram detail sheet, and Command Composer now automatically connect to selected gateway if not already connected. Shows red X icon with "Error!" status for 2 seconds on connection failures.
- **Connection Timeout Configuration** - Connection timeout now respects user settings across all connection types (tunneling/routing, plain/secure). All Rust connection functions accept timeout parameter passed from Flutter settings service.

---

## [1.6.1+23] - 2026-02-13

### Fixed
- **Disconnect Speed** - Fixed 10-second disconnect delay introduced in v0.11.0. Background tasks now stop before waiting for disconnect response, eliminating race condition. Disconnect completes in ~100-500ms while preserving send/recv performance improvements.
- **Hunt Connection UI** - Added loading indicators to connection FAB and status badge during connect/disconnect operations. Shows "Connecting..." or "Disconnecting..." with circular progress indicator, disabled during loading to prevent multiple simultaneous connection attempts.

---

## [1.6.0+22] - 2026-02-12

### Added
- **Variable Send Action** - New quick send action for Shark Hunt pages with runtime value input for up to 15 group addresses. Features multi-select GA picker with DPT validation and color-coded compatibility (red/yellow/green), DPT-specific input widgets for 25+ types (Boolean, Numeric, Time, Date, RGB/RGBW/xyY colors, Scene, etc.), and async execution with visual feedback. Optimized with Rust-side caching of parsed DPT and GAs.

### Fixed
- **KNX Routing Send** - Fixed GroupValueWrite/Read telegrams not appearing in ETS when sent via multicast routing. Corrected message code from L_Data.req (0x11) to L_Data.ind (0x29), source address from invalid 0.0.0 to configurable valid address (default: 15.15.255), and control field bits for KNX spec compliance. Added routing_source_address option to ClientOptions for customization.
- **Tutorial Overflow** - Resolved tooltip content overflow in tour steps 2 and 3 when using large fonts or display settings
- **Sheet Dismissal** - Fixed telegram detail, gateway details, settings, and quick send sheets expanding to full screen and blocking drag handles
- **Monitor Layout** - Corrected SliverAppBar height calculation to prevent overflow with scaled fonts
- **Gateway Display** - Fixed IP address text overflow in gateway rows on discover page

### Improved
- **Accessibility** - Enhanced support for maximum font sizes and display scaling across all screens
- **Tutorial Experience** - Shortened tour descriptions by 50-60% for better readability and reduced visual clutter
- **Bottom Sheets** - Added height constraints and scrolling to prevent full-screen expansion and ensure drag handles remain accessible
- **Dynamic Positioning** - Tutorial tooltips now adapt position based on text scale, automatically adjusting from -100px (normal) to -50px (large scale)

---

## [1.5.1+21] - 2026-02-05

### Added
- **CSV Export** - Export telegrams to CSV with draggable column configuration sheet for customizable data exports
- **Share Functionality** - Share telegrams and hunt cards directly from the app with dual Save/Share buttons
- **Keep Screen On** - Prevent idle screen timeout during monitoring with reactive wake lock management and settings toggle (defaults OFF)
- **Smart Filter Picker** - Quick access to telegram view settings with in-sheet navigation for easier filter management
- **Address Format Switching** - Toggle between 2-level and 3-level group address formats with floating badge on Monitor and Shark Hunt pages
- **Automatic Format Detection** - App automatically detects preferred address format from loaded ETS project files
- **Centralized Text Scaling** - Improved accessibility with standardized text scaling utilities across all widgets
- **ETS Project Integration** - Shark Hunt pages now display project status badge with info sheet, allowing quick project loading and unloading
- **Telegram Statistics** - View top 5 destinations/sources and APCI breakdown with progress bars in Monitor and Shark Hunt pages
- **Statistics Sheet Navigation** - Slide through statistics sections with lazy calculation and efficient caching

### Improved
- **Monitor Performance** - Optimized telegram filtering and batching for high-traffic scenarios with 50-100x faster address matching
- **FAB Controls** - Added cancel functionality during connection attempts with proper state synchronization
- **Send Badge** - Simplified to use bottom sheet with updated styling for better consistency
- **User Control** - Removed automatic monitor start from telegram detail sheet buttons for explicit user control
- **Text Accessibility** - Consistent text scaling limits applied throughout the app: content (1.0-2.0x), UI chrome (1.0-1.2x), icons (1.0-1.3x)
- **Monitor UI Polish** - Enhanced bottom sheets with Material cards, icons, and better visual hierarchy
- **Hunt Badge Design** - Updated all hunt badges to match monitor page styling with 8px radius and transparent backgrounds
- **Monitor Page Architecture** - Refactored into separate components for better maintainability (50% code reduction)
- **Statistics Visibility** - Increased initial sheet size to 50% with always-visible section headers for better discoverability
- **Framework Updates** - Upgraded to Flutter 3.38.9 with Dart 3.10.8 for latest performance improvements and bug fixes

### Fixed
- **Format Mismatch Filtering** - Resolved issue where 2-level addresses would not match telegrams displayed as 3-level
- **Quick Send Project Reference** - Command composer now receives correct project reference from quick send long press
- **CSV Export Handling** - Improved dynamic column selection with proper nullable field handling
- **Connection State** - Better synchronization between FAB cancel and connection state
- **Security Credential Checks** - Fixed backbone key validation, navigator locks, and dialog patterns in secure gateway selection
- **Localization** - Replaced hardcoded English strings in Shark Hunt widgets with proper localization keys
- **Text Overflow** - Added proper text protection (maxLines, overflow) throughout project and Shark Hunt pages

---

## [1.4.1+20] - 2026-01-30

### Added
- **Interactive Monitor Badges** - Added status badges for quick access to monitoring controls, telegram count, and gateway information with tap-to-view details
- **Clickable Building Elements** - Group addresses and devices in Buildings tab are now tappable, opening detail sheets for quick information access
- **Floating Filter Bar** - Filter bar now stays visible when scrolling through project tabs for easier access

### Improved
- **Error Notifications** - Monitor errors now appear as non-intrusive floating messages that auto-dismiss
- **Accessibility** - Better text scaling support and improved readability across all project views
- **Device Names** - Improved device name display in Buildings tab with proper fallback handling
- **Visual Consistency** - Standardized address format and improved icon clarity throughout the app

### Fixed
- **Search Functionality** - Device search now correctly finds devices with alternative name formats
- **Filter Behavior** - Fixed expansion of parent items when filtering by nested devices
- **Layout Issues** - Resolved overflow warnings in monitor page layout

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
