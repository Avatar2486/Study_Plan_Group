# Maven

## **FAANG-Level Maven Topics List (Complete Roadmap)**

### 1️⃣ Basics (Foundation)

- What is Maven? (Brief but clear)
- Maven vs Gradle (FAANG interviews love to ask this)
- Key Components:
    - `POM.xml`
    - Repository (Local, Central, Remote)
    - Build Lifecycle
    - Plugins vs Dependencies vs Goals
    - Convention over Configuration (Why Maven is opinionated)

---

### 2️⃣ Maven Lifecycle (Deep Dive)

- Phases:
    - Validate
    - Compile
    - Test
    - Package
    - Install
    - Deploy
- How lifecycle hooks work in FAANG-scale projects
- How plugins bind to lifecycle phases
- Custom lifecycle configurations (rare but asked in some companies)

---

### 3️⃣ Dependency Management (FAANG-Level Focus)

- Transitive Dependency Management (Diamond Problem in Maven)
- Dependency Scope:
    - Compile
    - Provided
    - Runtime
    - Test
    - Import (BOM Concept)
- Version Conflicts (Dependency Mediation)
- Exclusions & Optional Dependencies
- Dependency Tree Analysis (`mvn dependency:tree`)
- Managing versions with BOM (Bill of Materials)
- Dependency Locking (External Plugin)

---

### 4️⃣ Plugin Management (FAANG-Level Focus)

- Core Plugins vs Community Plugins
- Plugin Configuration (`<pluginManagement>` vs `<plugins>`)
- Common Plugins:
    - Compiler Plugin
    - Surefire Plugin (Unit Tests)
    - Failsafe Plugin (Integration Tests)
    - Dependency Plugin
    - Shade Plugin (Uber Jar)
    - Checkstyle, PMD, SpotBugs Plugins
- Writing Custom Plugins (if needed in interviews — rare)

---

### 5️⃣ Profiles (Real-World Usage)

- What are Maven Profiles?
- Profile Activation (Based on OS, Properties, Command Line, etc.)
- Use Cases:
    - Dev/QA/Prod profiles
    - Feature toggles via profiles
- Profile Conflicts (Who wins if multiple profiles apply?)

---

### 6️⃣ Multi-Module Projects (FAANG Must-Know)

- Parent POM vs Child POM
- Aggregator POM vs Inheritance POM
- Managing versions across modules
- Best Practices for Large Microservice Repos (Mono Repo using Maven)

---

### 7️⃣ Build Optimization & Performance Tuning

- Parallel Builds (`T 4C`)
- Remote Repository Caching (Nexus/Artifactory best practices)
- Dependency Download Optimizations
- Incremental Builds & Skip Phases (`Dmaven.test.skip=true`)

---

### 8️⃣ Maven Internal Workings (FAANG Focus)

- How Maven downloads dependencies (Transport & Checksum Validation)
- How Maven resolves versions (Nearest First Rule)
- What happens internally during each phase?
- Order of Execution (Lifecycles, Plugins, Profiles)

---

### 9️⃣ Advanced Configurations (Real-World Needs)

- Custom Properties (`<properties>` tag) & System Properties
- External Property Files (`maven-resources-plugin`)
- Using environment variables inside POM.xml
- Secrets management with Maven (not directly supported — best practices using `.mvn`)

---

### 🔟 Continuous Integration (FAANG Real Use Case)

- Maven with Jenkins, GitHub Actions, GitLab CI/CD
- Maven Caching in CI/CD (Critical in big tech)
- Running Maven in Docker (with caching & volume mount for `.m2`)

---

### 🧰 Debugging Maven Issues

- Dependency Tree Analysis
- Effective POM (`mvn help:effective-pom`)
- Debugging Plugins (`mvn -X`)
- Fixing Version Conflicts
- Understanding `Dependency Convergence` issues
- Diagnosing `Plugin Execution Not Covered` errors

---

### 💣 Common Interview Traps (FAANG)

- What if two transitive dependencies bring different versions of the same library? Who wins?
- How to override transitive dependency versions?
- What if two plugins bind to the same lifecycle phase?
- Difference between `<dependencyManagement>` and `<dependencies>`?
- How to completely skip tests in Maven?
- How to exclude a dependency from a specific module in a multi-module project?
- Maven vs Gradle (Real-world choice at scale)

---

### 💡 Real FAANG Scenarios (Important)

- How to create a fat jar (Uber jar) with Maven?
- How to create & use a Maven Archetype?
- How to publish artifacts to Nexus/Artifactory?
- How to write your own Maven Plugin?
- How to handle secrets/credentials in Maven?
- How to debug build failures in CI/CD (log analysis)

---

### 🔥 FAANG-Level Maven Interview Questions (Sample)

1. Explain the Maven Build Lifecycle and how plugins hook into it.
2. What is the difference between `dependencyManagement` and `dependencies`?
3. How does Maven resolve conflicting transitive dependencies?
4. How do you optimize Maven builds in large monorepos?
5. Explain the need for `maven-shade-plugin`. How does it work?
6. How do Maven Profiles work? What are some real-world scenarios where you used them?
7. How do you debug a `NoClassDefFoundError` in a Maven-built project?
8. How do you publish a custom library to an internal Nexus repository using Maven?
9. What’s the difference between `compile` and `provided` scope?
10. How does `mvn clean install` work in a multi-module project?

---

### ⚙️ Tools & Commands You Must Master

| Command | Purpose |
| --- | --- |
| `mvn clean install` | Full build cycle |
| `mvn dependency:tree` | Check dependency graph |
| `mvn help:effective-pom` | See full effective POM |
| `mvn versions:display-dependency-updates` | Check outdated dependencies |
| `mvn -T 4C clean install` | Parallel build |
| `mvn validate` | Pre-check build |
| `mvn -X` | Debug mode |
| `mvn help:describe` | Describe any plugin or goal |

---

### 📚 Study Resources (FAANG-Focused)

- Official Docs: [https://maven.apache.org/](https://maven.apache.org/)
- Blogs: Baeldung Maven Series
- YouTube: TechPrimers (Maven playlist)
- Mock Interviews: InterviewBit, LeetCode Discuss, Glassdoor
- Real Projects: Contribute to open-source Maven projects on GitHub