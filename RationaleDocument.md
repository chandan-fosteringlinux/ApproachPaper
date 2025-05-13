# Rationale Document

## Application Purpose

The application is designed to perform the following operations:

* Extract placeholder keys from a `.xml` file (e.g., `blueprint.xml`)
* Map these keys to corresponding key-value pairs present in a `.cfg` file
* Assign `null` to any key found in the `.xml` file but missing in the `.cfg` file
* Generate a `configMap.yml` file with the final set of key-value pairs

---

## Technology Stack Chosen

### Programming Language: Java

#### Reasons for Choosing Java

1. **Familiarity with Syntax and Concepts**
   I have a strong understanding of Java syntax, core concepts (such as file I/O, data structures, and exception handling), and best practices. This allows for faster development and debugging.

2. **Rich Ecosystem for File Parsing and Utilities**
   Java offers mature libraries and APIs (like `javax.xml.parsers`, `java.util.Properties`, etc.) that make XML parsing, configuration file reading, and file generation tasks seamless and efficient.

3. **Platform Independence and Portability**
   Java's platform-independent nature ensures that the application can run across different environments without significant changes.

4. **Strong Community Support**
   Java has a vast developer community and excellent documentation, which is helpful for troubleshooting and accessing best practices.

---

### Framework: Quarkus

#### Reasons for Choosing Quarkus

1. **Previous Experience and Familiarity**
   I have previously worked with the Quarkus framework and am well-acquainted with its build lifecycle, configuration, and extension ecosystem. This prior experience significantly reduced the ramp-up time.

2. **Fast Startup and Low Memory Footprint**
   Quarkus applications are lightweight and have fast startup times, which is beneficial even for command-line tools or background utilities.

2. **Ease of CLI**
   Quarkus provides seamless support for creating command-line applications using its `quarkus-picocli` extension. This matches the design and execution pattern of the current utility.

5. **Maven Integration**
   Quarkus integrates well with Maven, allowing for easy build, package (including `.deb`), and dependency management.

---

## Conclusion

Choosing **Java** as the programming language and **Quarkus** as the framework was a strategic decision driven by familiarity, project requirements, and the technical strengths of the tools. This combination enabled efficient development of a robust, portable, and maintainable application to automate the generation of `configMap.yml` files from `.xml` and `.cfg` configurations.
