# Trailblazer

> [!WARNING]
> This is the most shitty implementation this world has ever seen, and you should not use it.
> I made it to learn how to learn Maven & Java libraries. This is in no way related to the
> [C++ Trailblazer project](https://github.com/AlphaGameDeveloper/Trailblazer) I am currently
> working on. This repository is no longer maintained, and to be honest if you use it I would be
> both honored and questionning if you care about stability or maintainability in the slightest.

A powerful, flexible, and easy-to-use Java logging library that "just works" out of the box!

[![Gradle Package](https://github.com/AlphaGameDeveloper/Trailblazer/actions/workflows/gradle-publish.yml/badge.svg)](https://github.com/AlphaGameDeveloper/Trailblazer/actions/workflows/gradle-publish.yml)

## Features

- **Simple & Intuitive API** - Get started in seconds
- **Multiple Formatters** - Simple, JSON, and Columned output formats
- **Thread-Safe** - Safe for concurrent use
- **Configurable Log Levels** - DEBUG, INFO, WARN, ERROR, FATAL
- **Logger Factory** - Easy logger creation and management
- **Custom Output Streams** - Write to files, strings, or anywhere
- **Performance Optimized** - Level checking for expensive operations
- **Zero Configuration** - Works out of the box with sensible defaults

## Quick Start

### Basic Usage

```java
import dev.alphagame.trailblazer.LoggerFactory;
import dev.alphagame.trailblazer.TBLogger;

public class MyApp {
    private static final TBLogger logger = LoggerFactory.getLogger(MyApp.class);
    
    public static void main(String[] args) {
        logger.info("Application started");
        logger.warn("This is a warning");
        logger.error("An error occurred: %s", "sample error");
    }
}
```

### Different Formatters

```java
// Simple formatter (default)
TBLogger simpleLogger = LoggerFactory.createSimpleLogger("SimpleLogger");
simpleLogger.info("Simple formatted message");
// Output: [2025-01-20 10:30:45.123] [INFO] [SimpleLogger] Simple formatted message

// JSON formatter
TBLogger jsonLogger = LoggerFactory.createJSONLogger("JsonLogger");
jsonLogger.info("JSON formatted message");
// Output: {"level":"INFO","logger":"JsonLogger","message":"JSON formatted message","timestamp":1674213045123}

// Columned formatter
TBLogger columnLogger = LoggerFactory.createColumnedLogger("ColumnLogger");
columnLogger.info("Columned message");
// Output: INFO                |ColumnLogger         |Columned message     |
```

### Log Levels

```java
import dev.alphagame.trailblazer.LogLevel;

TBLogger logger = LoggerFactory.getLogger("MyLogger", LogLevel.DEBUG);

logger.debug("Debug message");
logger.info("Info message");
logger.warn("Warning message");
logger.error("Error message");
logger.fatal("Fatal message");

// Check if level is enabled (for performance)
if (logger.isDebugEnabled()) {
    logger.debug("Expensive operation result: %s", expensiveOperation());
}
```

### Custom Output Streams

```java
import java.io.FileOutputStream;
import java.io.PrintStream;

// Log to file
PrintStream fileStream = new PrintStream(new FileOutputStream("app.log"));
TBLogger fileLogger = LoggerFactory.createLoggerWithStream("FileLogger", fileStream);
fileLogger.info("This goes to a file");

// Log to string (for testing)
ByteArrayOutputStream baos = new ByteArrayOutputStream();
PrintStream stringStream = new PrintStream(baos);
TBLogger testLogger = LoggerFactory.createLoggerWithStream("TestLogger", stringStream);
testLogger.error("Test error");
String logOutput = baos.toString();
```

### Advanced Configuration

```java
import dev.alphagame.trailblazer.LoggerConfiguration;
import dev.alphagame.trailblazer.formatters.SimpleFormatter;

// Custom configuration
LoggerConfiguration config = new LoggerConfiguration(
    LogLevel.DEBUG, 
    new SimpleFormatter("yyyy-MM-dd HH:mm:ss")
);

TBLogger customLogger = LoggerFactory.getLogger("CustomLogger", config);

// Runtime configuration changes
customLogger.setLogLevel(LogLevel.WARN);
```

## API Reference

### LoggerFactory

The primary way to create loggers:

- `getLogger(String name)` - Get logger with default config
- `getLogger(Class<?> clazz)` - Get logger for a class
- `getLogger(String name, LogLevel level)` - Get logger with specific level
- `createSimpleLogger(String name)` - Create logger with SimpleFormatter
- `createJSONLogger(String name)` - Create logger with JSONFormatter
- `createColumnedLogger(String name)` - Create logger with ColumnedFormatter
- `createLoggerWithStream(String name, PrintStream stream)` - Custom output stream

### TBLogger

Main logging interface:

- `debug(String message, Object... args)` - Log debug message
- `info(String message, Object... args)` - Log info message
- `warn(String message, Object... args)` - Log warning message
- `error(String message, Object... args)` - Log error message
- `fatal(String message, Object... args)` - Log fatal message
- `isDebugEnabled()`, `isInfoEnabled()`, etc. - Check if level is enabled

### Log Levels

Available log levels (in order of severity):

1. `DEBUG` - Detailed information for debugging
2. `INFO` - General information messages
3. `WARN` - Warning messages
4. `ERROR` - Error messages
5. `FATAL` - Critical error messages

### Formatters

Built-in formatters:

- **SimpleFormatter** - Standard format with timestamp, level, logger name, and message
- **JSONFormatter** - JSON format for structured logging
- **ColumnedFormatter** - Fixed-width columned format

## Building

```bash
./gradlew build
```

## Testing

Run the example:

```bash
./gradlew compileTestJava
java -cp "build/classes/java/main:build/classes/java/test:build/dependencies/*" dev.alphagame.trailblazer.TrailblazerExample
```

## Installation

### Gradle

```gradle
dependencies {
    implementation 'dev.alphagame:trailblazer:VERSION'
}
```

### Maven

```xml
<dependency>
    <groupId>dev.alphagame</groupId>
    <artifactId>trailblazer</artifactId>
    <version>VERSION</version>
</dependency>
```

## License

This software is released under the MIT License. See [LICENSE](LICENSE) for details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.
