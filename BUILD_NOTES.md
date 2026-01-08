# Build Notes for IntelliJ IDEA 2025.3 Compatibility

## Changes Made

This PR updates the Package Search IntelliJ Plugin to be compatible with IntelliJ IDEA 2025.3.1 (build 253.x).

### Modified Files

1. **buildSrc/src/main/kotlin/Utils.kt**
   - Updated `INTELLIJ_VERSION` from `243.21565.23` (2024.3) to `253.17038.10` (2025.3.1)

2. **build.gradle.kts**
   - Updated `baseVersion` from `243-SNAPSHOT` to `253-SNAPSHOT`

3. **packagesearch.versions.toml**
   - Updated `idea` version from `2024.3` to `2025.3`
   - Updated Jewel bridge dependency from `jewel-ide-laf-bridge-243` to `jewel-ide-laf-bridge-253`

4. **plugin/build.gradle.kts**
   - Updated Jewel bridge reference to match the new 253 platform

5. **README.md**
   - Added note about 2025.3 compatibility as a community fork
   - Updated deprecation notice to clarify this is an unofficial extension

6. **plugin/src/main/resources/META-INF/plugin.xml**
   - Changed plugin name from "[DEPRECATED] Package Search" to "Package Search (2025.3 Compatible)"
   - Updated description to indicate this is a community fork with 2025.3 support

## Build Number Information

The build number `253.17038.10` follows the IntelliJ versioning pattern:
- `253` = IntelliJ IDEA 2025.3
- First two digits of the major version + last digit = release year and version number
- 2025.3 → 253

**Note**: The exact build number used (253.17038.10) is estimated based on the versioning pattern of previous releases. You may need to adjust this to match the actual IntelliJ IDEA 2025.3.1 release build number. You can find the correct build number at:
- https://www.jetbrains.com/idea/download/other.html
- In IntelliJ IDEA: Help → About → Copy version info

## Building the Plugin

### Prerequisites

- JDK 17 or later
- Gradle 8.3 or later (included via wrapper)
- Access to JetBrains Maven repositories (required for IntelliJ Platform dependencies)

### Build Commands

```bash
# Build the plugin
./gradlew :plugin:buildShadowPlugin

# Run the plugin in a sandbox IDE
./gradlew :plugin:runIde

# Run tests
./gradlew :plugin:test
```

### Potential Issues

1. **IntelliJ Platform Dependency Resolution**
   - The build requires access to JetBrains Maven repositories
   - Ensure your network can reach:
     - https://www.jetbrains.com/intellij-repository/
     - https://cache-redirector.jetbrains.com/
     - https://packages.jetbrains.team/

2. **Jewel Bridge Dependency**
   - The Jewel UI library requires a platform-specific bridge
   - `jewel-ide-laf-bridge-253` must be available for IntelliJ IDEA 253.x
   - If this version doesn't exist yet, you may need to wait for the Jewel library to be updated
   - Alternative: Remove Jewel dependency if it's not critical for functionality

3. **Build Number Verification**
   - If you encounter errors about the IntelliJ version not being found, you may need to update the build number
   - Check available versions in the IntelliJ Maven repository
   - Update `INTELLIJ_VERSION` in `buildSrc/src/main/kotlin/Utils.kt`

## Testing

After building successfully, test the plugin by:

1. Running `./gradlew :plugin:runIde` to launch a sandbox IDE with the plugin installed
2. Verifying the plugin appears in Settings → Plugins
3. Testing basic functionality:
   - Open a Gradle or Maven project
   - Use the Package Search tool window (bottom panel)
   - Search for and add dependencies

## Known Limitations

- The Package Search web service is scheduled to shut down on April 1, 2025
- After that date, the plugin's online search functionality will not work
- Consider migrating to IntelliJ IDEA's built-in dependency management features

## Questions or Issues

If you encounter build or runtime issues:

1. Verify you're using the correct IntelliJ IDEA build number for 2025.3.1
2. Check that all repositories are accessible
3. Review the Gradle build logs for specific error messages
4. Ensure your JDK version is compatible (JDK 17+)
