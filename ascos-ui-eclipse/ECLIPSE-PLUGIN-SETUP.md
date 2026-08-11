# Eclipse Plugin / Feature / Repository Setup

**Date**: August 11, 2026  
**Author**: GitHub Copilot  

---

## Overview

The `ascos-ui-eclipse` Maven module was converted from a bare skeleton into a fully structured
Eclipse / OSGi multi-module project built with **Tycho 4.0.10**.

References:
- [Tycho Reference Guide](https://www.eclipse.org/tycho/sitedocs/tycho-documentation.html)
- [Maven Tycho Eclipse Example](https://github.com/maxkratz/maven-tycho-eclipse-example)

---

## Module Structure

```
ascos-ui-eclipse/                           ← Tycho aggregator POM (packaging=pom)
├── ascos-ui-eclipse-plugin/               ← OSGi bundle (packaging=eclipse-plugin)
│   ├── pom.xml
│   ├── META-INF/
│   │   └── MANIFEST.MF
│   └── build.properties
├── ascos-ui-eclipse-feature/              ← Eclipse feature (packaging=eclipse-feature)
│   ├── pom.xml
│   ├── feature.xml
│   └── build.properties
└── ascos-ui-eclipse-repository/           ← p2 update site (packaging=eclipse-repository)
    ├── pom.xml
    └── category.xml
```

---

## Files Created / Modified

### Modified

| File | Change |
|------|--------|
| `ascos-ui-eclipse/pom.xml` | Replaced the plain Maven dependency on `ascos-core` with Tycho plugin management, target-platform environments, a p2 Eclipse release repository, and three submodule declarations. |

### Created

| File | Purpose |
|------|---------|
| `ascos-ui-eclipse-plugin/pom.xml` | Maven POM for the OSGi plugin (`eclipse-plugin` packaging). Maven `artifactId` aligned with the OSGi `Bundle-SymbolicName`. |
| `ascos-ui-eclipse-plugin/META-INF/MANIFEST.MF` | OSGi bundle manifest (`Bundle-SymbolicName: org.deventropy.ascos.ui.eclipse.plugin`). |
| `ascos-ui-eclipse-plugin/build.properties` | Tycho/PDE build properties — declares what gets included in the built plugin JAR. |
| `ascos-ui-eclipse-feature/pom.xml` | Maven POM for the Eclipse feature (`eclipse-feature` packaging). `artifactId` aligned with the feature `id`. |
| `ascos-ui-eclipse-feature/feature.xml` | Eclipse feature descriptor including the plugin as a component. Feature ID: `org.deventropy.ascos.ui.eclipse.feature`. |
| `ascos-ui-eclipse-feature/build.properties` | PDE build properties for the feature. |
| `ascos-ui-eclipse-repository/pom.xml` | Maven POM for the p2 update-site repository (`eclipse-repository` packaging). Declares a dependency on the feature. |
| `ascos-ui-eclipse-repository/category.xml` | p2 category descriptor — groups the feature under the `org.deventropy.ascos.category` install category. |

---

## Key Design Decisions

### Tycho Version
`4.0.10` — pinned in `ascos-ui-eclipse/pom.xml` under `<properties>` so all child modules inherit it.

### Eclipse Release Train
Target platform points to the **2026-06** Eclipse simultaneous release:
```
https://download.eclipse.org/releases/2026-06
```
This is configured as a p2 repository in `ascos-ui-eclipse/pom.xml`.

### Artifact ID ↔ OSGi ID Alignment
Tycho's `validate-id` goal requires the Maven `<artifactId>` to match the OSGi identity:

| Module | Maven artifactId | OSGi ID |
|--------|-----------------|---------|
| Plugin | `org.deventropy.ascos.ui.eclipse.plugin` | `Bundle-SymbolicName` in `MANIFEST.MF` |
| Feature | `org.deventropy.ascos.ui.eclipse.feature` | `id` attribute in `feature.xml` |
| Repository | `org.deventropy.ascos.ui.eclipse.repository` | (no OSGi ID requirement) |

### Multi-Platform Environments
The `target-platform-configuration` plugin is configured for four target environments:

| OS | WS | Arch |
|----|----|------|
| Linux | gtk | x86_64 |
| Windows | win32 | x86_64 |
| macOS | cocoa | x86_64 |
| macOS | cocoa | aarch64 |

---

## Build Output

After a successful `mvn clean verify -DskipTests` in `ascos-ui-eclipse/`:

| Artifact | Path |
|---------|------|
| Plugin JAR | `ascos-ui-eclipse-plugin/target/org.deventropy.ascos.ui.eclipse.plugin-0.0.1-SNAPSHOT.jar` |
| Feature JAR | `ascos-ui-eclipse-feature/target/org.deventropy.ascos.ui.eclipse.feature-0.0.1-SNAPSHOT.jar` |
| p2 Repository ZIP | `ascos-ui-eclipse-repository/target/org.deventropy.ascos.ui.eclipse.repository-0.0.1-SNAPSHOT.zip` |

---

## Build Commands

```bash
# Build only the Eclipse modules (from workspace root)
mvn clean verify -pl ascos-ui-eclipse -DskipTests

# Build all Eclipse submodules from within the aggregator directory
cd ascos-ui-eclipse
mvn clean verify -DskipTests

# Build with tests (none yet)
cd ascos-ui-eclipse
mvn clean verify
```

---

## Next Steps (Suggested)

1. **Add OSGi bundle for `ascos-core`** — Wrap `ascos-core` as an OSGi bundle so it can be
   declared as a `Require-Bundle` or `Import-Package` dependency in `MANIFEST.MF`.

2. **Add Eclipse extension points** — Implement views, commands, handlers, and menus via
   `plugin.xml` inside the plugin bundle.

3. **Add a `.target` platform file** — Pin exact Eclipse IU versions for fully reproducible builds
   and IDE target platform resolution.

4. **Add tests** — Add an `ascos-ui-eclipse-tests` module (`eclipse-test-plugin` packaging) for
   SWTBot or JUnit plug-in tests.

5. **Configure p2 deployment** — Set up a remote p2 repository URL for publishing the update site
   on releases.
