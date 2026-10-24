# 🧰 Node.js, npm & npx — Complete Command Cheat Sheet

![Node.js](https://img.shields.io/badge/Node.js-LTS-brightgreen)
![npm](https://img.shields.io/badge/npm-bundled-red)
![npx](https://img.shields.io/badge/npx-bundled-blue)
![License](https://img.shields.io/badge/License-MIT-yellow)

> A single, comprehensive reference for every command a Node.js developer needs — from installation and version management to package operations, publishing, security, and debugging.
>
> **Format:** Copy-paste ready · Beginner-friendly · Fully indexed

---

## 📋 Table of Contents

1. [Installation & Setup Commands](#1--installation--setup-commands)
2. [Version Management (nvm)](#2--version-management-nvm)
3. [Project Initialization](#3--project-initialization)
4. [Package Installation](#4--package-installation)
5. [Package Removal](#5--package-removal)
6. [Package Updates & Versioning](#6--package-updates--versioning)
7. [Listing & Inspecting Packages](#7--listing--inspecting-packages)
8. [Scripts & Execution](#8--scripts--execution)
9. [npx — Execute Without Installing](#9--npx--execute-without-installing)
10. [Security & Auditing](#10--security--auditing)
11. [Publishing Packages](#11--publishing-packages)
12. [npm Configuration](#12--npm-configuration)
13. [Cache Management](#13--cache-management)
14. [Workspaces (Monorepos)](#14--workspaces-monorepos)
15. [Node.js CLI Flags](#15--nodejs-cli-flags)
16. [Utility & Diagnostic Commands](#16--utility--diagnostic-commands)

---

## 1. 📦 Installation & Setup Commands

Commands to install **Node.js** and **npm** on each operating system.

## Windows

```powershell
# Method 1: Official Installer — download from https://nodejs.org

# Method 2: winget (Windows Package Manager)
winget install OpenJS.NodeJS.LTS

# Method 3: nvm-windows (multiple versions)
# Download from https://github.com/coreybutler/nvm-windows/releases
nvm install lts
nvm use lts

🧰 Node.js, npm & npx — Complete Command Cheat Sheet
> **Version:** 2.0  
> **Last Updated:** 2026  
> **Purpose:** A single, comprehensive reference for every command a Node.js developer needs — from installation and version management to package operations, publishing, security, and debugging.  
> **Format:** Copy-paste ready · Beginner-friendly · Fully indexed
---
📋 Table of Contents
Installation & Setup Commands
Version Management (nvm)
Project Initialization
Package Installation
Package Removal
Package Updates & Versioning
Listing & Inspecting Packages
Scripts & Execution
npx — Execute Without Installing
Security & Auditing
Publishing Packages
npm Configuration
Cache Management
Workspaces (Monorepos)
Node.js CLI Flags
Utility & Diagnostic Commands
Quick Reference Card
Common Errors & Fix Commands
---
1. 📦 Installation & Setup Commands
Commands to install Node.js and npm on each operating system.
Windows
```powershell
# Method 1: Official Installer — download from https://nodejs.org

# Method 2: winget (Windows Package Manager)
winget install OpenJS.NodeJS.LTS

# Method 3: nvm-windows (multiple versions)
# Download from https://github.com/coreybutler/nvm-windows/releases
nvm install lts
nvm use lts
```
macOS
```
# Method 1: Official Installer — download .pkg from https://nodejs.org

# Method 2: Homebrew (recommended)
brew install node

# Method 3: nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.zshrc
nvm install --lts
nvm use --lts
```
Linux (Ubuntu / Debian)
```
# Method 1: NodeSource PPA (latest version)
curl -fsSL https://deb.nodesource.com/setup_22.x | sudo -E bash -
sudo apt-get install -y nodejs

# Method 2: Default APT repository (older version)
sudo apt update && sudo apt install -y nodejs npm

# Method 3: nvm
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc
nvm install --lts
nvm use --lts
```
Linux (Arch / Fedora)
```
# Arch Linux
sudo pacman -S nodejs npm

# Fedora / RHEL
curl -fsSL https://rpm.nodesource.com/setup_22.x | sudo bash -
sudo dnf install -y nodejs
```
Verification After Installation
```
node -v          # → v20.x.x or v22.x.x
npm -v           # → 10.x.x or higher
npx -v           # → 10.x.x
```
---
2. 🔄 Version Management (nvm)
nvm lets you install, switch, and manage multiple Node.js versions without conflicts.28
Install & Switch Versions
```
# Install the latest LTS version
nvm install --lts

# Install a specific version
nvm install 20.11.0
nvm install 18.20.0
nvm install 16.20.2

# Install the latest release of a major version
nvm install 20

# Switch to a version
nvm use 20
nvm use 18.20.0
nvm use --lts
nvm use system          # Use the system-installed Node.js
```
List Versions
```
nvm ls                  # List all installed versions
nvm ls-remote           # List all available remote versions
nvm ls-remote --lts     # List only LTS versions available remotely
nvm current             # Show the currently active version
```
Set Default & Aliases
```
# Set default version for new shells
nvm alias default 20

# Create a custom alias
nvm alias myproject-version 18.20.0
nvm use myproject-version
```
Per-Project Version (`.nvmrc`)
```
# Create .nvmrc in project root
echo "20.11.0" > .nvmrc

# Use the version specified in .nvmrc
nvm use

# Install (if missing) then use
nvm install
```
> 💡 **Tip:** Add auto-switching to your shell by adding the `autoload_nvmrc` function to `~/.bashrc` or `~/.zshrc`.[28](https://raw.githubusercontent.com/OneUptime/blog/refs/heads/master/posts/2026-03-02-how-to-manage-multiple-nodejs-versions-on-ubuntu/README.md#1)
---
3. 🏁 Project Initialization
```
# Create package.json interactively (asks questions)
npm init

# Create package.json with defaults (skip all questions)
npm init -y

# Create with a specific scope / name
npm init --scope=@myorg

# Create a workspace package (see §14)
npm init -w ./packages/my-lib
```
Expected output (`npm init -y`):
```
{
  "name": "my-project",
  "version": "1.0.0",
  "main": "index.js",
  "scripts": { "test": "echo \"Error: no test specified\" && exit 1" },
  "keywords": [],
  "author": "",
  "license": "ISC"
}
```
---
4. 📥 Package Installation
Basic Installation
```
npm install                  # Install everything from package.json
npm i                        # Alias for npm install
npm install express          # Install a runtime dependency
npm install -D vitest        # Install a dev dependency (--save-dev)
npm install -E lodash        # Install with exact version (--save-exact)
npm install -O fsevents      # Install as optional dependency
npm install --no-save chalk  # Install without adding to package.json
npm install -g nodemon       # Install globally
```
Installation Flags (Reference)
Flag	Short	What It Does
`--save-dev`	`-D`	Adds to `devDependencies` (build tools, linters)
`--save-exact`	`-E`	Saves an exact version, no `^` or `~`
`--save-optional`	`-O`	Adds to `optionalDependencies`
`--save-peer`		Adds to `peerDependencies`
`--no-save`		Installs without modifying `package.json`
`--omit=dev`		Skips `devDependencies` (production install)
`--legacy-peer-deps`		Ignores peer dependency conflicts
`--global`	`-g`	Installs into npm’s global prefix
`--workspace=<name>`	`-w`	Targets a specific workspace (see §14)
`--workspaces`	`-ws`	Targets all workspaces
Install from Non-Registry Sources
```
npm install user/repo                 # GitHub repository
npm install user/repo#branch          # GitHub branch
npm install github:user/repo          # Explicit GitHub syntax
npm install gitlab:user/repo          # GitLab
npm install /path/to/local/folder     # Local folder
npm install ./archive.tgz             # Local tarball
npm install https://example.com/pkg.tgz  # Remote tarball
npm install @org/package              # Scoped package
npm install lodash@latest             # Latest tag
npm install lodash@4.17.21            # Specific version
npm install lodash@">=4 <5"           # Semver range
```
Clean Install (CI/CD)
```
npm ci    # Deletes node_modules, installs exactly from package-lock.json
          # Never modifies package.json or lockfile
```
> ✅ Use `npm ci` in CI/CD pipelines. Use `npm install` during development.
---
5. 🗑️ Package Removal
```
# Remove a local package
npm uninstall lodash

# Aliases (all equivalent)
npm remove lodash
npm rm lodash
npm r lodash

# Remove a dev dependency
npm uninstall -D vitest

# Remove a global package
npm uninstall -g nodemon

# Remove files but keep the entry in package.json
npm uninstall --no-save lodash

# Remove a workspace package
npm uninstall lodash -w backend
```
---
6. 🔄 Package Updates & Versioning
Update Installed Packages
```
npm update                  # Update all packages within semver ranges
npm update --save           # Also write new versions to package.json
npm update lodash           # Update a specific package
npm update -g               # Update all global packages
npm update -g nodemon       # Update a specific global package
npm install lodash@latest   # Force jump to the latest tag (across majors)
```
Check for Outdated Packages
```
npm outdated                # Show Current, Wanted, and Latest for each dep
npm outdated --global       # Show outdated global packages
npm outdated lodash         # Check a specific package
```
Expected output:
```
Package   Current  Wanted  Latest
lodash    4.17.20  4.17.21 5.0.0
```
Bump Package Version
```
npm version patch     # 1.2.3 → 1.2.4
npm version minor     # 1.2.3 → 1.3.0
npm version major     # 1.2.3 → 2.0.0
npm version 3.0.0     # Set an exact version
npm version prerelease --preid beta   # 1.2.3 → 1.2.4-beta.0
```
Interactive Update (npx)
```
npx npm-check-updates     # Check for newer versions
npx npm-check-updates -u  # Upgrade package.json to latest versions
```
---
7. 📋 Listing & Inspecting Packages
```
# Local packages
npm list                    # Full dependency tree
npm ls                      # Alias for npm list
npm list --depth=0          # Only top-level packages
npm list <package-name>     # Inspect a specific package

# Global packages
npm list -g                 # All global packages
npm list -g --depth=0       # Top-level global packages only

# Filtered listings
npm list --dev              # Only devDependencies
npm list --prod             # Only production dependencies
npm list --json             # JSON output

# Registry information
npm view lodash             # Registry metadata for a package
npm view lodash version     # Latest version only
npm view lodash versions    # All published versions
npm view lodash dependencies # Dependencies of a package
```
> 📌 `npm list --depth=0` is the most useful command for a quick overview of installed top-level packages.[5](https://last9.io/blog/npm-packages-cheatsheet/)
---
8. ⚙️ Scripts & Execution
Run Scripts Defined in `package.json`
```
npm run                 # List all available scripts
npm run dev             # Run the "dev" script
npm run build           # Run the "build" script
npm run lint            # Run the "lint" script
npm run lint --if-present   # Do nothing (without failing) if missing
npm start               # Shortcut for npm run start
npm test                # Shortcut for npm run test
npm stop                # Shortcut for npm run stop
```
Pass Arguments to Scripts
```
# Everything after "--" is passed to the underlying command
npm run build -- --mode staging
npm run test -- --watch
```
Run Scripts in Workspaces
```
npm run build -w frontend              # One workspace
npm run build --workspaces             # All workspaces
npm run build -ws --if-present         # All, skip missing scripts
```
> 💡 `npm start`, `npm test`, `npm stop`, and `npm restart` work **without** the `run` keyword.
---
9. ⚡ npx — Execute Without Installing
npx runs a package’s binary without permanently installing it.
```
# Run a tool directly
npx http-server .              # Start a local web server
npx prettier --write .         # Format code
npx eslint .                   # Lint JavaScript
npx ts-node script.ts          # Run TypeScript directly
npx esbuild app.js             # Bundle JavaScript
npx jsdoc .                    # Generate documentation
```
Scaffold New Projects
```
npx create-react-app my-app
npx create-next-app@latest
npx create-vite@latest
npx @angular/cli new my-app
```
Specify a Version or Package
```
npx create-vite@5.0.0 my-app        # Specific version
npx -p node@14 <command>            # Run with a different Node version
npx -p shellcheck which shellcheck  # Run a package and inspect its binary
```
> 🧠 `npx` checks local `node_modules/.bin` first, then downloads the package temporarily if not found.
---
10. 🔒 Security & Auditing
```
npm audit                     # Show known vulnerabilities
npm audit --json              # Machine-readable JSON output
npm audit --omit=dev          # Only check production dependencies
npm audit fix                 # Auto-fix compatible vulnerabilities (safe)
npm audit fix --force         # Force fixes, may include breaking major upgrades ⚠️
npm audit fix --dry-run       # Preview what --force would change
```
> ⚠️ **Warning:** `npm audit fix --force` can introduce **breaking changes**. Always review the output and test your project afterward.[44](https://www.volcengine.com/article/215627#1)
Additional Security Commands
```
npm doctor                    # Check environment health and common issues
npm ping                      # Verify registry connectivity
npm access list packages      # List packages you can access (for orgs)
```
---
11. 📤 Publishing Packages
Pre-Publish Checklist
```
npm login                     # Authenticate with the registry
npm whoami                    # Confirm logged-in user
npm version patch             # Bump version before publishing
npm pack                      # Create a tarball to inspect contents
npm publish --dry-run         # Simulate publish without uploading
```
Publish
```
npm publish                   # Publish with the "latest" tag
npm publish --tag beta        # Publish with a custom dist-tag[reference:16]
npm publish --access public   # Publish a scoped package publicly
```
Dist-Tags (Version Labels)
```
npm dist-tag add my-pkg@1.4.0 stable    # Tag a version
npm dist-tag rm my-pkg beta             # Remove a tag
npm dist-tag ls my-pkg                  # List all tags for a package
```
> 📌 By default, `npm publish` sets the **latest** tag. Use `--tag` to publish a prerelease or beta without affecting `latest`.[36](https://docs.npmjs.com/cli/v12/commands/npm-dist-tag)
Deprecate & Unpublish
```
npm deprecate my-pkg@"<1.0.0" "critical bug — upgrade to 1.x"
npm unpublish my-pkg@1.0.0    # Unpublish a specific version (within 72h)
```
Manage Owners
```
npm owner add username my-pkg
npm owner rm username my-pkg
npm owner ls my-pkg
```
---
12. ⚙️ npm Configuration
```
# View configuration
npm config list                 # Show all active settings
npm config list -l              # Include defaults
npm config list --json          # JSON output
npm config get registry         # Get a single value
npm config get prefix           # Show global install prefix

# Set configuration
npm config set registry https://registry.npmjs.org/
npm config set prefix '~/.npm-global'     # Avoid sudo for global installs
npm config set strict-ssl false           # Only for trusted corporate networks
npm config set proxy http://proxy:8080
npm config set https-proxy http://proxy:8080

# Delete configuration
npm config delete registry

# Edit the config file directly
npm config edit
```
> 🔑 **Key setting:** `npm config set prefix '~/.npm-global'` prevents `EACCES` permission errors during global installs.[54](https://docs.npmjs.com/cli/v12/commands/npm-config)
Common Config Keys
Key	Typical Value	Purpose
`registry`	`https://registry.npmjs.org/`	Package source
`prefix`	`~/.npm-global`	Global install directory
`strict-ssl`	`true` / `false`	SSL verification
`proxy` / `https-proxy`	Proxy URL	Corporate firewalls
`fund`	`false`	Disable funding messages
`audit`	`true` / `false`	Enable/disable audit on install
---
13. 🧹 Cache Management
```
npm cache verify              # Verify cache integrity
npm cache clean --force       # Clear the entire cache
npm cache add <package>       # Add a package to the cache manually
npm cache ls                  # List cache contents (deprecated but works)
```
> 🛠 Use `npm cache clean --force` when you encounter `EINTEGRITY` or corrupted install errors.
---
14. 🏗️ Workspaces (Monorepos)
npm workspaces let you manage multiple packages inside a single root project.
```
# Initialize a workspace
npm init -w ./packages/a

# Install a dependency into one workspace
npm install lodash -w backend
npm install -D vitest -w frontend

# Install a workspace as a dependency of another
npm install b -w a

# Run scripts across workspaces
npm run build -w frontend          # One workspace
npm run build --workspaces         # All workspaces
npm run build -ws --if-present     # All, skip missing scripts
npm run test --workspace=a         # Long form

# Uninstall from a workspace
npm uninstall lodash -w backend

# Clean install across all workspaces
npm ci
```
> 📌 The `--workspace` (`-w`) flag targets one workspace; `--workspaces` (`-ws`) targets all.
---
15. 🟢 Node.js CLI Flags
Basic Execution
```
node                          # Start the REPL (interactive shell)
node script.js                # Run a file
node -e "console.log('Hi')"   # Evaluate inline JavaScript
node -p "2 + 2"               # Evaluate and print the result
node -c script.js             # Syntax-check without executing
node --check script.js        # Same as -c
```
Information & Help
```
node -v                       # Print Node.js version
node --version                # Same
node -h                       # Print help
node --help                   # Same
node --v8-options             # List all V8 engine options
```
Watch Mode (Node 18+)
```
node --watch script.js        # Auto-restart on file changes
node --watch-path=./src app.js # Watch a specific directory
```
Environment Variables
```
node --env-file=.env app.js   # Load environment variables from a file
```
Debugging & Inspection
```
node inspect script.js        # Start the built-in debugger
node --inspect app.js         # Enable Chrome DevTools debugging (port 9229)
node --inspect-brk app.js     # Break on the first line
node --prof app.js            # Generate a V8 CPU profile
node --trace-deprecation app.js  # Show stack traces for deprecations
node --throw-deprecation app.js  # Throw errors for deprecations
```
Module & Path Resolution
```
node --preserve-symlinks app.js   # Use symlink paths instead of real paths
node -r dotenv/config app.js      # Preload a module at startup
```
> 💡 `node` with no arguments opens the **REPL** — useful for quick experiments.
---
16. 🔧 Utility & Diagnostic Commands
```
npm doctor                    # Run health checks on your npm environment
npm ping                      # Check registry connectivity
npm root                      # Show local node_modules path
npm root -g                   # Show global node_modules path
npm exec -- <command>         # Run a local package executable
npm prefix                    # Show local project prefix
npm prefix -g                 # Show global prefix
npm explain <package>         # Explain why a package is installed
npm why <package>             # Alias for npm explain
npm fund                      # Show funding information for dependencies
npm rebuild                   # Rebuild native modules
```
---
