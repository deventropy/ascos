# GitHub Copilot Instructions for Deventropy Ascos Project

## Project Overview


### Project Purpose


## Architecture Overview

### Modular Structure


### Architectural Layers


## Technology Stack

### Core Technologies


### Code Generation & Processing


### Serialization & Processing


### Logging


### UI Frameworks


### Testing Frameworks


## Code Style & Conventions

### Naming Conventions


### Formatting Guidelines


### Code Organization


### Library and Framework Usage

#### Using Lombok


#### Using MapStruct


## Design Patterns & Principles

### Applied Patterns


### SOLID Principles


### Clean Architecture


## Common Tasks & How-To

### Building the Project

```bash
# Build all modules
mvn clean install

# Build specific module
mvn clean install -pl bls-dm-core

# Check for dependency updates
mvn clean install -P version-check

# Build without tests
mvn clean install -DskipTests
```

## Testing

### Test Organization


### Testing Frameworks


### Test Naming Conventions


### Test Coverage Guidelines


### Test Conventions


### Test Execution


## Important Directories & Files


## Performance Considerations


## Security Considerations


## Future Enhancements & Extensibility

### Planned Features


### Extensibility Guidelines


## Development Environment Setup

### Prerequisites


### Initial Setup


### IDE Configuration


### Debugging


## Documentation Standards


## Continuous Integration


## License


## Quick Reference Commands

```bash
# Clean and build
mvn clean install

# Run specific test
mvn test -Dtest=FrameCalculatorTest

# Skip tests
mvn install -DskipTests

# Update dependencies
mvn versions:display-dependency-updates

# Build JavaFX app
mvn clean install -pl bls-dm-ui-javafx

# Check for vulnerabilities
mvn dependency-check:check

# Format code
mvn spotless:apply  # if configured

# Generate site documentation
mvn site:site
```

## Getting Help


## LLM Model Preferences for Copilot



---

**Last Updated**: August 7, 2026
**Project Version**: 0.0.1-SNAPSHOT
**Java Version**: 25 (LTS)