# WAR Repackager Project

This project takes an existing WAR file and repackages it with minimal overrides — most notably a custom `web.xml` — without altering the original contents.

## 🧩 What it does

- Unzips the original WAR from `src/main/original/monapp.war`
- Injects a custom `WEB-INF/web.xml` (from `src/main/webapp/WEB-INF/`)
- Repackages everything into a clean new WAR in `target/`

✅ No changes to `src/main/java`  
✅ No Maven repository publishing required  
✅ No side effects on the original WAR

---

## 🗂️ Project Structure

```
src/
├── main/
│   ├── original/ # Place the original .war file here
│   │   └── cmod-rest.war
│   └── webapp/
│       └── WEB-INF/
│           └── web.xml # Your override file
```

---

## 🚀 How to build

```bash
mvn clean package
```

This produces the patched WAR under:

```php-template
target/<artifactId>-<version>.war
```

You can rename it via the <finalName> setting in pom.xml if needed.

## 🛠️ Customization

* Want to override more files?
→ Add them to src/main/webapp/ in the correct subfolders.

* Want to switch WAR source?
→ Replace cmod-rest.war in src/main/original/.

## 🧠 Why this setup?

* Keeps everything in src/main/, as any Java developer would expect
* Doesn't pollute src/main/webapp with extracted content
* Fully automatable, clean, and IDE-friendly
* Does not require installing the original WAR into the local Maven repo

## ☕ Requirements

* Maven 3.6+
* JDK 8+ (only for build, not needed if you don’t compile any Java class)

## Tomcat integration

Does work only with Tomcat 9.X, not with 10.x or 11.x. Why? Because of WebSphere, and how the cmod-rest.api was built, it doesn't support the new JEE, which requires to rename a lot of packages from javax to jakarta.
Until IBM does the correction, or the upgrade... we will need to stay on Tomcat 9.x. Of course, one way would be to decompile, correct and recompile :-) but this is not allowed :-D

### setenv.sh

Here is a sample of my setenv.sh that works and needs to be installed in the <tomcat_install_dir>/bin/setenv.sh (in linux, please adapt to your own plateform)

```bash
export CMOD_HOME=/opt/ibm/ondemand/V10.5
export JAVA_HOME=${CMOD_HOME}/jre
export JRE_HOME=${JAVA_HOME}
export restcfgdir="/home/user/CMOD_REST/rest_cfg_dir"
export CATALINA_OPTS="$CATALINA_OPTS -Djava.library.path=${CMOD_HOME}/www:${CMOD_HOME}/lib64"
export CLASSPATH="${CMOD_HOME}/jars/log4j-core-2.23.1.jar:${CMOD_HOME}/jars/log4j-api-2.23.1.jar:${CMOD_HOME}/jars/gson-2.10.1.jar:${CMOD_HOME}/jars/commons-pool2-2.12.0.jar:${CMOD_HOME}/www/api/ODApi.jar"
```

## 📬 Questions?
Feel free to reach out or fork the project.
This setup is ideal for patching black-box WAR files without rewriting or reverse-engineering them.

