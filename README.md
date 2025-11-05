# WORKING ON IT

# AxTpa - Advanced TPA Plugin for Minecraft

Professional TPA (Teleport Ask) plugin for Minecraft 1.20.1 with multi-server support, GUI, combat detection, and full customization.

## 📋 Minecraft Versions & Compatibility

- **Primary Target**: Minecraft 1.20.1
- **Server Software**: Paper (Recommended), Spigot, Purpur, Folia
- **Java Version**: Java 17+ (Required)
- **API Version**: 1.20

See [VERSIONS.md](VERSIONS.md) for detailed compatibility information.


## ✨ Features

### Core Functionality
- ✅ Complete TPA command system (`/tpa`, `/tpahere`, `/tpaccept`, etc.)
- ✅ Interactive GUI with player information display
- ✅ Combat detection (prevents TPA during PvP)
- ✅ Trap detection (flight and void detection)
- ✅ Configurable countdown with Titles/ActionBar support
- ✅ Movement detection (cancels teleport if player moves)

### Advanced Features
- ✅ Multi-server support (BungeeCord/Velocity)
- ✅ Database support (H2, SQLite, MySQL)
- ✅ Player blocking system
- ✅ Auto-accept TPA requests
- ✅ PlaceholderAPI integration
- ✅ Fully customizable GUI
- ✅ Clickable chat buttons
- ✅ Configurable sounds and messages
- ✅ Cooldown system
- ✅ World blocking
- ✅ Configuration reload command

### Security & Safety
- 🛡️ Combat protection
- 🛡️ Trap detection (void, flying)
- 🛡️ Movement cancellation
- 🛡️ Player blocking
- 🛡️ World restrictions

## 📦 Commands

| Command | Description | Permission |
|---------|-------------|------------|
| `/tpa <player>` | Request teleport to a player | `axtpa.use` |
| `/tpahere <player>` | Request player to come to you | `axtpa.use` |
| `/tpaccept [player]` | Accept a TPA request | `axtpa.use` |
| `/tpdeny [player]` | Deny a TPA request | `axtpa.use` |
| `/tpacancel` | Cancel your pending request | `axtpa.use` |
| `/tpalist` | List pending requests | `axtpa.use` |
| `/tpatoggle` | Toggle TPA requests on/off | `axtpa.use` |
| `/tpablock <player>` | Block a player | `axtpa.use` |
| `/tpaunblock <player>` | Unblock a player | `axtpa.use` |
| `/tpalistblocked` | List blocked players | `axtpa.use` |
| `/tpaauto` | Toggle auto-accept | `axtpa.use` |
| `/axtpareload` | Reload plugin configuration | `axtpa.reload` |

## 🔐 Permissions

- `axtpa.*` - All permissions (OP by default)
- `axtpa.use` - Basic permission to use TPA commands (all by default)
- `axtpa.admin` - Administrative permissions (OP by default)
- `axtpa.bypass` - Bypass all restrictions (OP by default)
- `axtpa.bypass.combat` - Bypass combat restriction (OP by default)
- `axtpa.bypass.cooldown` - Bypass cooldown (OP by default)
- `axtpa.bypass.toggle` - Bypass player toggle (OP by default)
- `axtpa.bypass.block` - Bypass player blocking (OP by default)
- `axtpa.reload` - Reload configuration (OP by default)

## 🚀 Installation

### Requirements
- **Minecraft**: 1.20.1
- **Server**: Paper (recommended), Spigot, or compatible fork
- **Java**: 17 or higher
- **Dependencies**: Automatically downloaded by Paper on first load

### Server Installation

1. Download the latest JAR from releases
2. Place it in your server's `plugins/` folder
3. Restart the server (Paper will automatically download required libraries)
4. The plugin will automatically generate `config.yml`
5. Configure the database according to your needs

### Compilation (For Developers)

```bash
mvn clean package
```

The compiled JAR will be in `target/AxTpa-X.X.X-BETA.jar`

**Note**: The JAR is ultra lightweight (~60KB). Dependencies are loaded separately by Paper.

## ⚙️ Configuration

### Database Configuration

The plugin supports three database types:

#### H2 (Default - Local file)
```yaml
database:
  type: "H2"
```

#### SQLite (Local file)
```yaml
database:
  type: "SQLITE"
```

#### MySQL (Multi-server)
```yaml
database:
  type: "MYSQL"
  host: "localhost"
  port: 3306
  database: "axtpa"
  username: "root"
  password: "your_password"
  pool-size: 10
  connection-timeout: 30000
```

### Multi-Server Support

To enable TPA between different servers (BungeeCord/Velocity):

```yaml
messaging:
  enabled: true
  channel: "axtpa:main"
```

**Note:** For cross-server TPA, you need:
- BungeeCord or Velocity on the proxy
- MySQL configured (doesn't work with H2/SQLite between servers)
- Plugin installed on all servers

### GUI Configuration

Customize the GUI appearance:

```yaml
gui:
  enabled-tpa: true # Show GUI for normal TPA
  enabled-tpahere: true # Show GUI for TPAHere
  title: "&6&lTPA Request"
  accept-button-material: "GREEN_CONCRETE"
  deny-button-material: "RED_CONCRETE"
  filler-material: "GRAY_STAINED_GLASS_PANE"
```

### Countdown Display

Configure how the countdown is displayed:

```yaml
tpa:
  teleport-delay: 5 # Wait time in seconds
  countdown-display: "both" # none, title, actionbar, both
  countdown-title: "&e&l{time}"
  countdown-subtitle: "&7To &e{destination} &7| {info}"
  countdown-actionbar: "&eTeleporting to &6{destination} &ein &6{time} &eseconds..."
```

## 📊 PlaceholderAPI Support

Requires PlaceholderAPI plugin installed.

### Available Placeholders

| Placeholder | Description | Example |
|-------------|-------------|---------|
| `%axtpa_pending_requests%` | Number of pending TPA requests | `2` |
| `%axtpa_cooldown%` | Remaining cooldown in seconds | `15` |
| `%axtpa_toggle_status%` | Toggle status (Enabled/Disabled) | `Enabled` |
| `%axtpa_blocked_count%` | Number of blocked players | `3` |
| `%axtpa_auto_accept_status%` | Auto-accept status | `Disabled` |

### Usage Examples

```
# In a scoreboard plugin
Line 1: "&7Pending requests: &e%axtpa_pending_requests%"
Line 2: "&7Cooldown: &e%axtpa_cooldown%&7s"
Line 3: "&7TPA: &a%axtpa_toggle_status%"

# In a chat plugin
Format: "&7[TPA: &a%axtpa_toggle_status%&7]"
```

## 🔄 TPA Flow

### Normal TPA Request:
1. Player A sends `/tpa PlayerB`
2. PlayerB receives chat notification
3. PlayerB uses `/tpaccept` to open GUI (if enabled)
4. PlayerB sees information and accepts/denies
5. If accepted, 5-second countdown (configurable)
6. If player doesn't move, successful teleport

### TPAHere Flow:
1. Player A sends `/tpahere PlayerB`
2. PlayerB receives GUI automatically (if enabled)
3. PlayerB accepts/denies in GUI
4. Countdown and teleport

### Auto-Accept:
1. Player A sends `/tpa PlayerB`
2. If PlayerB has auto-accept enabled:
   - Automatically accepted (if not in combat)
   - Countdown starts directly
   - Teleport after countdown

## 🛡️ Security Features

### Combat Detection
- Players cannot use TPA while in combat
- Configurable wait time after combat (default: 15 seconds)

### Trap Detection
- Checks if target player is flying
- Checks if player is in void (trap indicator)
- Shows warnings in GUI

### Blocked Worlds
Block TPA usage in certain worlds:

```yaml
tpa:
  blocked-worlds:
    - "pvp_arena"
    - "combat_zone"
```

## 🎨 Customization

### Messages
All messages are customizable in `config.yml`:

```yaml
messages:
  prefix: "&8[&6AxTpa&8] &r"
  request-sent: "&aYou have sent a TPA request to &e{player}&a."
```

### Sounds
Configure sounds for different events:

```yaml
tpa:
  sounds:
    request-sent: "ENTITY_PLAYER_LEVELUP"
    request-received: "BLOCK_NOTE_BLOCK_PLING"
    request-accepted: "ENTITY_EXPERIENCE_ORB_PICKUP"
```

## 📝 Changelog

### Version 1.2.0
- Added `/axtpareload` command for configuration reload
- Added GUI enable/disable options for TPA and TPAHere
- Enhanced GUI customization (materials, colors, positions)
- Improved countdown display with destination information
- Fixed TPA flow for better user experience
- All messages translated to English

### Version 1.1.0
- Added player blocking system
- Added auto-accept feature
- Added PlaceholderAPI integration
- Improved GUI functionality

### Version 1.0.0
- Initial release
- Core TPA functionality
- Multi-server support
- Database support

## 🐛 Troubleshooting

### Common Issues

1. **Database error**: Check credentials in `config.yml`
2. **Cross-server TPA not working**: Ensure MySQL is configured and BungeeCord/Velocity is active
3. **GUI not opening**: Use `/tpaccept` to open GUI (doesn't open automatically for normal TPA)
4. **Placeholders not working**: Make sure PlaceholderAPI is installed
5. **Player heads not appearing**: Plugin is compatible with offline mode, but may require additional configuration

## ⚡ Optimization

The plugin is fully optimized to prevent memory leaks:
- ✅ All periodic tasks are cancelled correctly
- ✅ Listeners are unregistered when not needed
- ✅ Database connections are closed properly
- ✅ GUIs are cleaned up when player disconnects
- ✅ Empty lists are automatically removed

## 📋 Requirements

- **Minecraft Version**: 1.20.1
- **Server Software**: Spigot/Paper 1.20.1
- **Java Version**: 17 or higher
- **Optional Dependencies**: 
  - PlaceholderAPI (for placeholders)
  - BungeeCord/Velocity (for multi-server support)

## 📄 License

This plugin was developed for AXTrial Space.

## 👤 Author

**Axxtrial**

---

**Version:** 1.2.0  
**Minecraft:** 1.20.1  
**Java:** 17+  
**Status:** Actively Maintained
