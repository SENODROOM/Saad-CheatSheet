# Converting from `nodemon app.js` to `npm run dev`

This guide walks you through the process of converting your Node.js application from running with `nodemon app.js` to using the standard `npm run dev` command.

## Overview

- **Current method**: `nodemon app.js` (direct nodemon command)
- **Target method**: `npm run dev` (npm script command)
- **Benefits**: Standardized development workflow, easier team collaboration, better project documentation

## Step 1: Install nodemon as a development dependency

First, ensure nodemon is installed in your project dependencies:

```bash
npm install --save-dev nodemon
```

**Why?** Installing nodemon as a dev dependency ensures it's available for development but doesn't bloat your production deployment.

## Step 2: Update package.json scripts

Add a `dev` script to your `package.json` file:

```json
{
  "scripts": {
    "start": "node app.js",
    "dev": "nodemon app.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  }
}
```

**Example for MD Pharmacy project:**

```json
{
  "name": "md-pharmacy-api",
  "version": "1.0.0",
  "description": "GeeksForGeeks",
  "main": "app.js",
  "scripts": {
    "start": "node app.js",
    "dev": "nodemon app.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "MD",
  "license": "ISC",
  "devDependencies": {
    "nodemon": "^3.0.1"
  },
  "dependencies": {
    "axios": "^1.7.3",
    "cors": "^2.8.5",
    "dotenv": "^16.4.5",
    "express": "^4.18.2",
    "fuse.js": "^7.0.0",
    "mongoose": "^8.0.3",
    "morgan": "^1.10.0",
    "multer": "^1.4.5-lts.1",
    "node-cron": "^3.0.3",
    "nodemailer": "^6.9.14",
    "pushbullet": "^3.0.0",
    "xlsx": "^0.18.5"
  }
}
```

## Step 3: Create nodemon configuration (Optional but Recommended)

Create a `nodemon.json` file in your project root for better configuration:

```json
{
  "watch": ["./"],
  "ext": "js,json",
  "ignore": ["node_modules/", "*.log"],
  "delay": "1000",
  "env": {
    "NODE_ENV": "development"
  }
}
```

**Configuration options explained:**
- `watch`: Directories/files to watch for changes
- `ext`: File extensions to monitor
- `ignore`: Files/directories to ignore
- `delay`: Delay in milliseconds before restarting
- `env`: Environment variables for development

## Step 4: Update your development workflow

### Old workflow:
```bash
cd backend
nodemon app.js
```

### New workflow:
```bash
cd backend
npm run dev
```

## Step 5: Update documentation

Update your README.md or project documentation to reflect the new command:

**Before:**
```bash
cd backend
npm install
nodemon app.js
```

**After:**
```bash
cd backend
npm install
npm run dev
```

## Step 6: Verify the setup

Test that everything works correctly:

1. Start the development server:
   ```bash
   npm run dev
   ```

2. Make a small change to `app.js` and save it
3. Verify that nodemon automatically restarts the server
4. Check that your application still works as expected

## Additional Tips

### For team projects
- Add `nodemon` to `devDependencies` in `package.json`
- Commit the updated `package.json` and `package-lock.json`
- Include the `nodemon.json` configuration file if created

### For different environments
You can create multiple scripts for different scenarios:

```json
{
  "scripts": {
    "start": "node app.js",
    "dev": "nodemon app.js",
    "dev:debug": "nodemon --inspect app.js",
    "dev:verbose": "nodemon --verbose app.js"
  }
}
```

### Common nodemon options
- `--inspect`: Enable Node.js debugging
- `--verbose`: Show detailed logging
- `--config`: Specify custom config file
- `--exec`: Run with different command (e.g., `ts-node` for TypeScript)

## Troubleshooting

### Issue: `npm run dev` not found
**Solution**: Ensure you've added the `dev` script to `package.json` and run `npm install` to update dependencies.

### Issue: Nodemon not restarting on file changes
**Solution**: Check your `nodemon.json` configuration and ensure the files you're editing are in the `watch` directory.

### Issue: Port already in use
**Solution**: Either stop the previous process or configure nodemon to use a different port in your environment variables.

## Final Result

After completing these steps, you'll have:
- A standardized development command (`npm run dev`)
- Better project documentation
- Easier onboarding for new team members
- Configurable development environment

The conversion maintains all the benefits of nodemon while following npm best practices for script management.
