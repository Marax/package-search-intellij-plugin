# Testing Checklist for IntelliJ IDEA 2025.3 Compatibility

This checklist should be completed once the plugin is built in an environment with access to JetBrains Maven repositories.

## Pre-Build Verification

- [ ] Verify the correct IntelliJ IDEA 2025.3.1 build number
  - Current value: `253.17038.10`
  - Check at: https://www.jetbrains.com/idea/download/other.html
  - Update `INTELLIJ_VERSION` in `buildSrc/src/main/kotlin/Utils.kt` if needed

- [ ] Verify Jewel bridge compatibility
  - Current dependency: `jewel-ide-laf-bridge-253`
  - Check if this version exists in the Jewel repository
  - May need to update to a different version or remove Jewel dependency if not available

## Build Verification

- [ ] Clean build succeeds
  ```bash
  ./gradlew clean
  ./gradlew :plugin:buildShadowPlugin
  ```

- [ ] No compilation errors
- [ ] No dependency resolution errors
- [ ] Plugin JAR is created in `plugin/build/distributions/`

## Runtime Testing

### Basic Functionality

- [ ] Plugin loads in IntelliJ IDEA 2025.3.1
  ```bash
  ./gradlew :plugin:runIde
  ```

- [ ] Plugin appears in Settings → Plugins
- [ ] Package Search tool window is visible (View → Tool Windows → Package Search)
- [ ] No exceptions in IDE log (Help → Show Log in Finder/Explorer)

### Maven Project Testing

- [ ] Open a Maven project
- [ ] Package Search tool window opens successfully
- [ ] Can browse and search for dependencies
- [ ] Can add a dependency to pom.xml
- [ ] Dependency is correctly added with proper syntax

### Gradle Project Testing

- [ ] Open a Gradle (Groovy DSL) project
- [ ] Package Search tool window opens successfully  
- [ ] Can browse and search for dependencies
- [ ] Can add a dependency to build.gradle
- [ ] Dependency is correctly added with proper syntax

- [ ] Open a Gradle (Kotlin DSL) project
- [ ] Package Search tool window opens successfully
- [ ] Can browse and search for dependencies
- [ ] Can add a dependency to build.gradle.kts
- [ ] Dependency is correctly added with proper syntax

### Kotlin Multiplatform Testing

- [ ] Open a KMP project
- [ ] Package Search recognizes KMP structure
- [ ] Can add dependencies to correct source sets
- [ ] Dependencies are correctly added

### Edge Cases

- [ ] Plugin works with multiple projects open
- [ ] Plugin survives IDE restart
- [ ] Settings are persisted between sessions
- [ ] No memory leaks (check memory usage over time)

## Known Issues to Watch For

Since this is an updated version of a deprecated plugin:

1. **Web Service Shutdown**
   - Note: The Package Search web service shuts down April 1, 2025
   - Test what happens when the service is unavailable
   - Verify graceful degradation

2. **API Compatibility**
   - Check if all IntelliJ Platform APIs used are still available in 253.x
   - Watch for deprecation warnings in build
   - Test areas that might use changed APIs:
     - Project model
     - Dependency management
     - UI components

3. **Jewel UI Library**
   - If using Jewel for UI, ensure it renders correctly
   - Check dark and light themes
   - Verify high DPI displays work correctly

## Regression Testing

Compare behavior with 2024.3 version:

- [ ] Same features work
- [ ] No new bugs introduced
- [ ] Performance is similar or better
- [ ] UI looks consistent

## Sign-off

- [ ] All tests pass
- [ ] No critical bugs found
- [ ] Plugin is ready for use
- [ ] Documentation updated with any findings

## Reporting Issues

If issues are found:

1. Check if the IntelliJ build number needs adjustment
2. Check if any dependencies need version updates
3. Review the Gradle build output for warnings
4. Check IntelliJ IDEA logs for exceptions
5. Document the issue with:
   - IntelliJ IDEA version (exact build number)
   - Plugin version  
   - Steps to reproduce
   - Expected vs actual behavior
   - Relevant log output
