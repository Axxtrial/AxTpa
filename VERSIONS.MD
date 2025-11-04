# AxTpa - Supported Minecraft Versions

## Minecraft Versions

AxTpa is designed to work with **Minecraft 1.20.1** and is compatible with Paper, Spigot, and their forks.

### Tested Versions
- ✅ **Minecraft 1.20.1** (Primary target)
- ✅ **Paper 1.20.1** (Recommended)
- ✅ **Spigot 1.20.1**

### Compatibility Notes

#### Server Software Support
- **Paper** (Recommended): Full support including automatic library loading
- **Spigot**: Full support with manual library management
- **Purpur**: Full support (Paper-based)
- **Folia**: Should work, but not extensively tested

#### Java Version Requirements
- **Minimum**: Java 17
- **Recommended**: Java 17 or higher

#### API Version
- **API Version**: 1.20 (as specified in `plugin.yml`)

### Multi-Server Support
- ✅ **BungeeCord**: Supported via plugin messaging
- ✅ **Velocity**: Supported via plugin messaging

### Database Support
- ✅ **H2**: Default, file-based database
- ✅ **SQLite**: Recommended for production
- ✅ **MySQL**: Recommended for multi-server setups

### Dependencies
AxTpa uses Paper's automatic library loading system. The following libraries are automatically downloaded:
- H2 Database (2.2.224)
- SQLite JDBC (3.44.1.0)
- MySQL Connector/J (8.2.0)
- HikariCP (5.1.0)

All dependencies are downloaded automatically on first plugin load when using Paper.

### Performance Notes
- Optimized for servers with 50-500+ concurrent players
- Efficient database queries with proper indexing
- Memory leak-free design with proper cleanup on player disconnect
- Lightweight: ~60KB JAR file (dependencies loaded separately)

### Future Version Support
Support for other Minecraft versions may be added in the future based on community demand.

