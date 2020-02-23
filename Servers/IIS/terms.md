## IIS Terms
- **IIS**: Internet Information Services (was Server before)
- **Application Pool**: a logical container where website will work inside. Each site can work on its own application pool
or multiple sites may use the same application pool. Isolation is the main reason to use application pools. It is possible
even devide a content of one website (different directories) into different Application Pools. In this way parts of your
site may be isolated (one part can still run if another is down).
- **Virtual Directory**: a directory which is not physically located in the same directory as the webstite. Say you need a
common directory in both sites with some sorts of Terms of Use html files. Just provide a path to the `virtual directory`
to get content of that directory for each website.
- **Web Platform Installer**: (Web PI) is a freeware, package management system that
installs non-commercial development tools and their dependencies that are part of Microsoft Web Platform.
