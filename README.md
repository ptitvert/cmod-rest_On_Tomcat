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

src/
├── main/
│ ├── original/ # Place the original .war file here
│ │ └── monapp.war
│ └── webapp/
│ └── WEB-INF/
│ └── web.xml # Your override file


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
→ Replace monapp.war in src/main/original/.

## 🧠 Why this setup?

* Keeps everything in src/main/, as any Java developer would expect
* Doesn't pollute src/main/webapp with extracted content
* Fully automatable, clean, and IDE-friendly
* Does not require installing the original WAR into the local Maven repo

## ☕ Requirements

* Maven 3.6+
* JDK 8+ (only for build, not needed if you don’t compile any Java class)


## 📬 Questions?
Feel free to reach out or fork the project.
This setup is ideal for patching black-box WAR files without rewriting or reverse-engineering them.

