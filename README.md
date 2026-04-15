# m2d - macOS Virtual Display Manager

<p align="center">
  <img src="Resources/Assets.xcassets/AppIcon.appiconset/icon_128x128.png" alt="m2d Icon" width="64" height="64">
</p>

<p align="center">
  <a href="#features">Features</a> •
  <a href="#ui-layout">UI Layout</a> •
  <a href="#requirements">Requirements</a> •
  <a href="#installation">Installation</a> •
  <a href="#usage">Usage</a>
</p>

A lightweight macOS virtual display management tool. Create virtual Retina displays, manage HiDPI resolutions, and control them via menu bar GUI or CLI.

---

## Features

### Core Features (v1.0)

- Create virtual displays with custom resolutions
- HiDPI/Retina support (1920×1080, 2560×1440, 3840×2160)
- Multiple refresh rates (30/60/120/144 Hz)
- Menu bar integration for quick access
- Create/delete virtual displays via popover menu
- Display status and count in menu bar

### Enhanced Features (v1.1)

- Preset configurations (Work, Reading, Presentation, Gaming)
- CLI tool support (`m2d-cli start`, `m2d-cli stop`, `m2d-cli list`, `m2d-cli create` etc.)

---

## UI Layout

### 2.1 Menu Bar Popover View (StatusMenuView)

**Popover Width**: 380 pixels

The menu bar popover provides quick access to all m2d features without opening the main window.

```
┌──────────────────────────────────────────────────────────┐
│ m2d                                    📊 3/5  🕐 60 Hz │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐   │
│  │     ⛶        │  │     ≡        │  │     ⚙        │   │
│  │  Create VD   │  │ Arrangement  │  │   Settings   │   │
│  └──────────────┘  └──────────────┘  └──────────────┘   │
│                                                          │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  Displays                                               │
│                                                          │
│  🖥️ Built-in Retina Display                             │
│     2560×1440 • 60 Hz                                   │
│                                                          │
│  🟦 Virtual #1  [○]  [★]                                │
│     1920×1080 • HiDPI • 60 Hz                           │
│                                                          │
│  🟦 Virtual #2  [○]  [★]                                │
│     2560×1440 • HiDPI • 120 Hz                          │
│                                                          │
├──────────────────────────────────────────────────────────┤
│                                            [🗑️ Remove All]│
│                                             [⏻ Quit]     │
└──────────────────────────────────────────────────────────┘
```

**Status Header**:
- Rounded app icon (24×24)
- App name "m2d"
- **Display Counter**: Shows current/total displays (e.g., "3/5" means 3 active out of 5 maximum)
- **Refresh Rate**: Current primary refresh rate (e.g., "60 Hz")

**Quick Actions Section**:
- **Create VD**: Primary action button (blue background, white text) - opens Create Display Wizard
- **Arrangement**: Opens macOS System Settings → Displays
- **Settings**: Opens Settings window

**Display List Section**:
- **Physical Displays**: Gray monitor icon, display name, resolution, refresh rate
- **Virtual Displays**: Blue display name (editable via double-click), resolution, HiDPI badge, refresh rate
- **Inline Editing**: Double-click virtual display name to edit (TextField with save/cancel buttons)
- **Main Display Badge**: Blue "Main" label on primary display
- **Toggle Switch**: iOS-style toggle to enable/disable virtual displays
- **Star Button**: Toggle favorite (orange filled star = saved, gray outline star = not saved)

**Bottom Actions**:
- **Remove All**: Red text button (only visible when virtual displays exist)
- **Quit**: Gray bordered button to exit the application

---

### 2.2 Settings Window (SettingsView)

**Window Dimensions**: 520 × variable height (based on content)

The settings window uses a sidebar navigation pattern with three preference panels.

```
┌─────────────────────────────────────────────────────────────────┐
│ Settings                                                        │
├──────────┬──────────────────────────────────────────────────────┤
│          │                                                      │
│ General  │  App Language                                        │
│ Displays │  ○ System Default  ○ English  ○ 中文                │
│ About    │  Requires app restart to take effect                 │
│          │                                                      │
│          │ ─────────────────────────────────────────────────── │
│          │                                                      │
│          │  Launch at Login                                     │
│          │  [✓] Auto-start m2d on login                        │
│          │  Automatically start m2d when you log in             │
│          │                                                      │
│          │ ─────────────────────────────────────────────────── │
│          │                                                      │
│          │  Menu Bar                                            │
│          │  [✓] Show virtual display count                     │
│          │  [✓] Show current refresh rate                      │
│          │                                                      │
│          │ ─────────────────────────────────────────────────── │
│          │                                                      │
│          │  Maximum Virtual Displays                           │
│          │  ○ 1  ○ 2  ○ 4                                      │
│          │  Maximum number of virtual displays that...          │
│          │                                                      │
│          │ ─────────────────────────────────────────────────── │
│          │                                                      │
│          │  System Auto Login                                   │
│          │  ● Enabled                                          │
│          │  Current User: username                              │
│          │  [Open System Settings...]                           │
│          │                                                      │
├──────────┴──────────────────────────────────────────────────────┤
│                                           [Cancel]  [Done]      │
└─────────────────────────────────────────────────────────────────┘
```

**Sidebar Navigation**:
- **General**: App language, launch settings, menu bar display options, maximum displays, system auto-login
- **Displays**: Virtual display management and deletion
- **About**: Application version, links, and credits

**General Settings Panel**:

| Setting | Options | Description |
|---------|---------|-------------|
| App Language | System Default / English / 中文 | UI language (requires restart) |
| Launch at Login | Toggle | Auto-start m2d on system login |
| Show Display Count | Toggle | Show "N/M" in menu bar header |
| Show Refresh Rate | Toggle | Show current Hz in menu bar header |
| Max Virtual Displays | 1 / 2 / 4 | Maximum concurrent virtual displays |
| System Auto Login | Status indicator + link | Show macOS auto-login status |

**Displays Settings Panel**:
- Lists all active virtual displays
- Each entry shows: icon, name, "Main" badge, resolution, refresh rate, HiDPI status
- Delete button (destructive, red icon) for each display
- Empty state message: "No virtual displays created yet"

**About Panel**:
- App icon (64×64)
- Application name and version number
- Link to GitHub Issues
- Link to Discussions
- License information

---

### 2.3 Create Display Wizard (CreateDisplayWizard)

**Window Dimensions**: 520 × 650 pixels

A two-step wizard for creating virtual displays with comprehensive configuration options.

#### Step 1: Resolution, Scale and Refresh Rate Selection

```
┌─────────────────────────────────────────────────────────────────┐
│ Create Virtual Display                              ○ ○         │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Select Resolution                                              │
│                                                                 │
│  ★ Recommended  📁 Work  📖 Reading  🎮 Gaming  🎬 Presentation │
│                                                                 │
│  ┌─────────────────────┐  ┌─────────────────────┐              │
│  │  ★                  │  │                     │              │
│  │  1600×1200          │  │  2160×1440          │              │
│  │  📁 4:3            │  │  📁 3:2            │              │
│  │  @2x                │  │  @2x                │              │
│  └─────────────────────┘  └─────────────────────┘              │
│                                                                 │
│  ┌─────────────────────┐  ┌─────────────────────┐              │
│  │                     │  │                     │              │
│  │  2560×1600          │  │  Custom  [+]        │              │
│  │  🎬 16:10           │  │                     │              │
│  │  @2x                │  │                     │              │
│  └─────────────────────┘  └─────────────────────┘              │
│                                                                 │
│ ─────────────────────────────────────────────────────────────── │
│                                                                 │
│  Scale                                                          │
│  [  1x  ][  2x  ][  3x  ]                                      │
│                                                                 │
│ ─────────────────────────────────────────────────────────────── │
│                                                                 │
│  Refresh Rate                                                   │
│  Select the refresh rate for your virtual display               │
│                                                                 │
│  [  30 Hz  ][  60 Hz  ][ 120 Hz  ][ 144 Hz  ]                  │
│                                                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ 🟢 Smooth (60 Hz)                                       │   │
│  │ Good balance of performance and quality. Recommended    │   │
│  │ for most users.                                         │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

**Resolution Selection Area**:
- **Usage Scenario Legend**: Horizontal scrollable legend showing icon + label for each scenario
- **Resolution Grid**: 2-column lazy grid with preset cards
- **Preset Card Content**:
  - "Recommended" badge (orange, top-left) if applicable
  - Logical resolution (e.g., "1920×1080")
  - Usage scenario icon + Aspect ratio (e.g., 📁 16:9, 📖 4:3)
  - Scale factor badge (e.g., "@2x")
- **Custom Resolution Button**: Blue bordered card with "+" icon
- **Usage Scenario Icons**:
  - ★ Recommended (orange star)
  - 📁 Work (16:9, briefcase)
  - 📖 Reading (4:3, book)
  - 🎮 Gaming (16:9, game controller)
  - 🎬 Presentation (16:10, film reel)

**Scale Selection**:
- **Segmented Picker**: 3-segment control for 1x, 2x, 3x scale factors
- Determines the logical vs. backing pixel ratio for Retina displays

**Refresh Rate Selection**:
- **Segmented Picker**: 4-segment control for 30/60/120/144 Hz (available rates vary by resolution)
- **Information Card**:
  - Icon + Title (e.g., "Smooth (60 Hz)")
  - Description text
  - GPU Impact Indicator: 4-bar meter (green → blue → orange → red)
  - Impact level text: Low / Medium / High / Very High

#### Custom Resolution Sheet

```
┌──────────────────────────────────────────────────────────┐
│ Custom Resolution                                 ×      │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  Width    Height                                         │
│  [___]  ×  [___]                                        │
│  (640-5120)   (480-2880)                                │
│                                                          │
│  Live Preview                                           │
│  ┌──────────────────────────────────────────────────┐   │
│  │ Resolution:  1920×1080  [@2x]                    │   │
│  │ Pixels:      3840×2160                           │   │
│  │ Aspect Ratio: 16:9                               │   │
│  │ [████████████████████]  •  Display Shape         │   │
│  └──────────────────────────────────────────────────┘   │
│                                                          │
│  ┌──────────────────────────────────────────────────┐   │
│  │ ● Resolution is valid, ready to create display   │   │
│  └──────────────────────────────────────────────────┘   │
│                                                          │
│  [Cancel]                                  [Next →]     │
└──────────────────────────────────────────────────────────┘
```

**Custom Resolution Form**:
- **Dimension Inputs**: Number fields for Width (640-5120) and Height (480-2880)
- **Live Preview Section**:
  - Resolution with scale factor badge (e.g., "@2x")
  - Actual pixel dimensions
  - Aspect ratio value
  - Visual preview rectangle showing display shape
- **Validation Section**: Success (green check) or error (red X) with message
- **Action Buttons**: Cancel / Next

#### Step 2: Confirmation

```
┌──────────────────────────────────────────────────────────┐
│ Create Virtual Display                              ○ ○   │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  Confirm Configuration                                  │
│                                                          │
│  ┌────────────────────────────────────────────────────────┐   │
│  │ Resolution:    1920×1080  [HiDPI @2x]                 │   │
│  │ Pixels:       3840×2160                                │   │
│  │ Refresh Rate: 60 Hz                                    │   │
│  └────────────────────────────────────────────────────────┘   │
│                                                          │
│  ┌────────────────────────────────────────────────────────┐   │
│  │ ● Ready                                               │   │
│  │ System is ready to create virtual displays            │   │
│  └────────────────────────────────────────────────────────┘   │
│                                                          │
│  [Show Diagnostics]                                      │
│                                                          │
└──────────────────────────────────────────────────────────┘
│  [Back]                                     [Create]       │
└──────────────────────────────────────────────────────────┘
```

**Configuration Summary Card**:
- **Resolution**: Shows logical resolution + HiDPI badge + scale factor (e.g., "@2x")
- **Pixels**: Shows backing pixel dimensions (e.g., "3840×2160")
- **Refresh Rate**: Shows Hz value

**System Status Card**:
- **Ready (Green)**: "System is ready to create virtual displays"
- **Issues (Orange)**: Shows warning icon, problem list, recommended actions, "Request Permissions" button
- **Unsupported (Red)**: Shows X icon, "Your system configuration is not supported"
- **Checking (Gray)**: Shows question mark, "Checking system compatibility..."

**Footer Actions**:
- **Back**: Navigate to step 1 (disabled on step 1, shows "Cancel" instead)
- **Next**: Navigate to step 2 (disabled on step 2)
- **Create**: Execute display creation (shows progress ring when creating)

---

### 2.5 Display Arrangement View (DisplayArrangementView)

Opens the system Settings Displays to configure arrangement.

---

## Requirements

### System Requirements

| Requirement | Minimum | Recommended |
|-------------|---------|-------------|
| macOS | 14.0 (Sonoma) | 26.0 (Tahoe) |
| Architecture | Intel / Apple Silicon | Apple Silicon (M1/M2/M3/M4/M5) |
| Swift | 5.9+ | 5.9+ |
| RAM | 2 GB | 4 GB+ |
| GPU | Integrated graphics | Dedicated GPU (for 120/144 Hz) |

### Required Permissions

Virtual displays require specific system permissions to function properly:

**Screen Recording Permission (Required)**

- **Location**: System Settings → Privacy & Security → Screen Recording
- **Purpose**: Allows the app to create and manage virtual displays
- **When prompted**: Grant permission when the dialog appears during display creation
- **Detection**: App automatically detects missing permissions and shows "Request Permissions" button

**Accessibility Permission (Optional)**

- **Location**: System Settings → Privacy & Security → Accessibility
- **Purpose**: Enables advanced display management features like automatic arrangement
- **When to use**: Only needed for special display arrangements and hotkey functionality

**Permission Request Flow**:
1. App detects missing permissions during startup or display creation
2. User is prompted to grant permissions through UI
3. System opens relevant preference panes automatically
4. Display creation proceeds after permissions are granted

---

## Installation

### From DMG (Recommended)

1. Download `m2d-x.x.x.dmg` from [Releases](../../releases)
2. Double-click to mount the disk image
3. Drag `m2d.app` to your Applications folder
4. Launch m2d from Applications or Spotlight
5. Grant Screen Recording permission when prompted

---

## Usage

### Menu Bar

m2d runs as a menu bar app. Click the m2d icon (📊) in your menu bar to access:

- **Virtual display count and status**: Shows current/total displays and primary refresh rate
- **Quick actions**: Create VD, Arrangement (System Settings), Settings
- **List of all displays**: Physical and virtual displays with toggle switches
- **Remove All**: Delete all virtual displays at once

### Creating Virtual Displays

1. Click the m2d menu bar icon
2. Click the "Create VD" button (blue primary button)
3. **Step 1 - Select Resolution**:
   - Choose a preset resolution or click "Custom"
   - Select refresh rate (30/60/120/144 Hz)
   - Review GPU impact indicator
4. **Step 2 - Confirm**:
   - Verify configuration summary
   - Check system status (green = ready)
   - Click "Create Display"
5. If prompted, grant Screen Recording permission in System Settings
6. The virtual display will appear in your display list

### CLI Commands

```bash
# Start the m2d background application
m2d-cli start

# Stop m2d and remove all virtual displays
m2d-cli stop

# List all virtual displays
m2d-cli list

# Create a virtual display
m2d-cli create --width 1920 --height 1080 --refresh-rate 60 --hidpi

# Create with custom name
m2d-cli create --width 2560 --height 1440 --refresh-rate 120 --name "My Virtual Display"

# Remove a virtual display by ID
m2d-cli remove <display-id>

# Enable a virtual display
m2d-cli enable <display-id>

# Disable a virtual display
m2d-cli disable <display-id>

# Favorite (save) a virtual display
m2d-cli favorite <display-id>

# Unfavorite a virtual display
m2d-cli unfavorite <display-id>

# Show help
m2d-cli --help
```
---

## Troubleshooting

### Virtual Display Creation Fails

**Permission Errors**:
- Grant Screen Recording permission in System Settings → Privacy & Security → Screen Recording
- If the app doesn't appear in the list, quit and restart the app, then try creating again
- Use the "Request Permissions" button in the creation dialog for automatic setup

**"Display not registered in system" Error**:
- Ensure Screen Recording permission is granted
- Wait a few seconds and try again
- Check System Report → Graphics/Displays to verify display detection

**App Shows Permission Warnings**:
- Click "Request Permissions" in the creation dialog
- This will open System Settings automatically
- Grant permissions and restart the app if needed

### Performance Issues

**High GPU Usage with 120/144 Hz**:
- Lower refresh rate to 60 Hz for integrated graphics
- Reduce number of virtual displays
- Close other GPU-intensive applications

**Display Not Appearing in System Settings**:
- Wait 5-10 seconds for macOS to detect the display
- Click "Refresh" in the display list
- Try creating a new virtual display

---

## Support

- [Issues](../../issues) - Bug reports and feature requests
- [Discussions](../../discussions) - Q&A and general discussion
- [Wiki](../../wiki) - Documentation and tutorials

---

<p align="center">
  Made with ❤️ for macOS users
</p>
