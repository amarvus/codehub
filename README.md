# CodeHub

**Project Status: In Progress**

---

## 🚀 Features

- `init` ➝ Initialize a repository (`.codehub/`)
- `add <file>` ➝ Add a file to staging (WIP)
- `commit <message>` ➝ Commit staged files (WIP)
- `push` ➝ Push commits to S3 (WIP)
- `pull` ➝ Pull commits from S3 (WIP)
- `revert <commitID>` ➝ Revert to a previous commit (WIP)

---

## 📦 How It Works (Concept Recap)

### ✅ `index.js`

This is the **main file** using `yargs` to handle CLI commands.

- **`yargs`**: Library to build command-line tools
- **`hideBin(process.argv)`**: Removes `node` and script name from args
- **`.command(...)`**: Registers a CLI command
- **`.positional(...)`**: Defines required argument like `<file>`
- **`.demandCommand()`**: Ensures user types a command
- **`.help().argv`**: Adds `--help` and starts CLI parser

### Example:

```bash
node index.js init
node index.js add myfile.txt
node index.js commit "Initial commit"

```

---

## ✅ initRepo in controllers/init.js
Initializes a .codehub folder in the current directory and sets up the config.

Key Concepts:

| Code                                      | What it Does                                  |
| ----------------------------------------- | --------------------------------------------- |
| `path.resolve(...)`                       | Builds absolute path (safe across OS)         |
| `path.join(...)`                          | Joins folders and filenames into a valid path |
| `process.cwd()`                           | Gets the current working directory            |
| `fs.promises.mkdir(..., recursive: true)` | Creates folder (and parent if needed)         |
| `fs.promises.writeFile(...)`              | Writes content to a file                      |
| `process.env.S3_BUCKET`                   | Reads environment variable for S3 bucket      |
| `.codehub/config.json`                    | File that stores bucket config                |


---

Output Folder:
After node index.js init, you get:
.codehub/
├── config.json   ← contains {"bucket": "your-bucket-name"}
└── commits/      ← empty folder to store commit files

---

Quick Revision

| Concept          | Explanation                                                |
| ---------------- | ---------------------------------------------------------- |
| `yargs`          | For parsing CLI commands                                   |
| `hideBin()`      | Removes junk from `process.argv` before parsing            |
| `.command()`     | Declares a command like `init`, `add` etc.                 |
| `.positional()`  | Declares required argument like `<file>`                   |
| `fs.promises`    | For async file system operations like `mkdir`, `writeFile` |
| `path.join()`    | Joins path segments safely (cross-platform)                |
| `path.resolve()` | Converts relative path to absolute                         |
| `process.cwd()`  | Gets current working directory                             |
| `process.env.X`  | Reads environment variable                                 |
| `.codehub/`      | Acts like `.git/` to store repo data                       |

---

🌐 Running the CLI
Install dependencies (if using packages like yargs):
```
npm install yargs
```
Run commands:
```
node index.js init
node index.js add file.txt
node index.js commit "Add file"
```
