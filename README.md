**Project 3: Build Automation of Java Application using Maven**

**Project Description**
In this project, I demonstrated how to automate the build lifecycle of a Java application using Apache Maven on an AWS EC2 (Amazon Linux 2023) environment. The goal was to move away from manual compilation and use a standardized tool to handle project structure, dependencies, and artifact generation.

**Technical Environment**
- Cloud Platform: AWS (EC2 Instance)
- Operating System: Amazon Linux 2023
- Build Tool: Apache Maven 3.8.4
- Language: Java 17 (Amazon Corretto)

**Step-by-Step Implementation**
**Step 1: Environment Configuration**
First, I accessed the server as a root user to ensure I had the necessary permissions for installation and configuration:
Bash
sudo su -

I verified the Maven installation to confirm it was correctly linked to the Java 17 runtime:
Bash
mvn -version

**Step 2: Generating the Project Structure**
Instead of creating directories manually, I used a Maven Archetype (a project template). This automatically created a standard folder structure including src/main/java for my code and src/test/java for testing.

**Command used:**
Bash
mvn archetype:generate -DgroupId=com.mycompany.app -DartifactId=my-app -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false

**Result:** A new directory named my-app was created with a pre-configured pom.xml file.

**Step 3: Troubleshooting Version Mismatch**
When I first attempted to build the project, the build failed with a Compilation Error:
“Source option 5 is no longer supported. Use 7 or later.”

**The Issue:** The default Maven template was set to use an older Java version (Source 5), while my system was running Java 17.
**The Fix:** I used the vi editor to modify the pom.xml file. I added the following compiler properties to explicitly tell Maven to use Java 17:

XML
<properties>
    <maven.compiler.source>17</maven.compiler.source>
    <maven.compiler.target>17</maven.compiler.target>
</properties>

**Step 4: Executing the Build Lifecycle**
After fixing the configuration, I ran the command to clean the project and package the code into an executable format:
Bash
mvn clean package

- clean: Removed any previous build artifacts to ensure a fresh start.
- package: Compiled the code and bundled it into a JAR file.
- Outcome: The terminal displayed "BUILD SUCCESS".

**Step 5: Verification of the Build Artifact**
After the build, I verified the output inside the target/ directory:
Bash
ls -l target/

I found the generated file: my-app-1.0-SNAPSHOT.jar.

Finally, I executed the application to confirm it worked as expected:

Bash
java -cp target/my-app-1.0-SNAPSHOT.jar com.mycompany.app.App

**Output Received:** Hello World!

**Key Learnings**:-
- **Automation:** Understood how Maven simplifies the development workflow by automating repetitive tasks.
- **POM Management:** Learned that pom.xml is the "brain" of a Maven project where all settings and dependencies are managed.
- **Problem Solving:** Successfully identified and resolved a Java version compatibility issue, which is a common real-world DevOps challenge.
- **Artifacts:** Learned that a .jar file is the final "Artifact" that DevOps engineers deploy to various environments.

**How to Run This Project Locally**:-

-Clone this repository.
-Ensure you have Maven and JDK 17 installed.
-Run mvn clean package.
-Execute the JAR file located in the target folder.
