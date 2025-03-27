# Node.js Development Environment Setup

## Current Installation Status
- **Node.js**: v23.9.0 (installed via pacman)
- **npm**: v11.2.0 (installed via pacman)
- **pnpm**: v10.7.0 (installed globally via npm)
- **npx**: Available (comes with npm)

## Installation Process
1. **Node.js Installation**
   - Already installed via pacman
   - Package: `nodejs` (23.9.0-1)
   - Type: "Current" release

2. **npm Installation**
   ```bash
   sudo pacman -S npm
   ```
   - Installed npm and its dependencies:
     - node-gyp (11.1.0-3)
     - nodejs-nopt (7.2.1-1)
     - semver (7.7.1-1)
     - npm (11.2.0-1)

3. **pnpm Installation**
   ```bash
   sudo npm install -g pnpm
   ```
   - Installed globally via npm
   - Version: 10.7.0

## Available Commands
- `node` - Run JavaScript files
- `npm` - Node Package Manager
- `pnpm` - Alternative Package Manager
- `npx` - Execute Node.js packages

## Usage Examples
1. **Create a new project**
   ```bash
   npm init
   # or
   pnpm init
   ```

2. **Install packages**
   ```bash
   npm install <package>
   # or
   pnpm add <package>
   ```

3. **Run Node.js files**
   ```bash
   node <filename>
   ```

4. **Run packages directly**
   ```bash
   npx <package>
   ```

## Notes
- All tools are properly installed and ready to use
- Global packages require sudo permissions for installation
- The setup is complete and ready for Node.js development 