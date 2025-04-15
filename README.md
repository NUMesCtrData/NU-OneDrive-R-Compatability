## 📂 Platform-Independent OneDrive Connection in R

This snippet detects whether the user is running the program on **Windows** or **Mac**, and sets up the correct file path to the **OneDrive - Northwestern University** folder. This allows file operations (read/write) across both platforms without needing to modify paths manually.

---

### 🔧 How It Works

- Detects the operating system (Windows or macOS).
- Determines the user's NetID (username).
- Constructs the appropriate path to the user's OneDrive and shared data directories.
- Stores these paths in two reusable variables:
  - `od_loc`: OneDrive path
  - `sp_dm_loc`: SharePoint Data Management path

---

### 💻 Code

```r
# 🌐 Detect System and Set OneDrive Path

# Windows:
if (Sys.info()[['sysname']] == "Windows") {
  netid <- Sys.info()["user"]
  
  # Identify the OneDrive path
  od_loc <- paste("C:/Users/", netid, "/OneDrive - Northwestern University/", sep = "")
  
  # Identify the Mesulam Data Management SharePoint
  sp_dm_loc <- paste("C:/Users/", netid, "/Northwestern University/", sep = "")
}

# Mac:
if (Sys.info()[['sysname']] == "Darwin") {
  netid <- Sys.info()["user"]
  
  # Identify the OneDrive path
  od_loc <- paste("/Users/", netid, "/OneDrive - Northwestern University/", sep = "")
  
  # Identify the Mesulam Data Management SharePoint
  sp_dm_loc <- paste("/Users/", netid, "/Northwestern University/", sep = "")
}
```

---

### ✅ Why This is Useful

- **Cross-platform compatibility**: Avoids hardcoding paths that break on other systems.
- **Reusable logic**: Paths are dynamically created based on user and system.
- **Plug-and-play**: Drop this block at the top of your R scripts to simplify file operations for multiple users on different machines.

---

### 📝 Notes

- Assumes OneDrive is installed and synced on the user’s machine.
- Paths will automatically match the NetID of the currently logged-in user.
- You can now use `od_loc` and `sp_dm_loc` throughout your script for reading/writing files, e.g.:

```r
read.csv(paste0(od_loc, "data/my_dataset.csv"))
write.csv(results, paste0(sp_dm_loc, "outputs/summary.csv"))
```
