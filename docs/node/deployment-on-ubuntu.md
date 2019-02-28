Deployment on Ubuntu 16.04
==========================

Guide for manual production deployment of node.js server on Ubuntu 16.04.

# Step 1: App versioning

Before doing release you have to understand the system versioning. One of the
 standard for this is at https://semver.org/ and https://docs.npmjs.com/about-semantic-versioning

To bump version your server, follow Node.js's guideline at https://docs.npmjs.com/cli/version.html
```bash
npm version <patch|minor|major>
```

- MAJOR version when you make incompatible API changes,
- MINOR version when you add functionality in a backwards-compatible manner, and
- PATCH version when you make backwards-compatible bug fixes.

Push code to git
```bash
git push origin master
git push --tags
```

# Step 2: Setup your server

- Access server via SSH, then follow https://github.com/nodesource/distributions/blob/master/README.md#installation-instructions
 to install Node.js. It is recommended to use LTS version for stable performance
  and high compatibility with other libraries.

- Install git
```bash
sudo apt-get update
sudo apt-get install git
```

- Install pm2
```bash
npm install -g pm2
```

# Step 3: Clone your code base to server using git

```bash
mkdir /var/www/my-app
cd /var/www/my-app
git clone <your-git-url>
```

# Step 4: Install npm packages and start server

- Install npm packages
```bash
npm install
```

Here your server is ready to run. It's recommended to use pm2 to run the server.

- To start pm2 the first time
```bash
NODE_ENV=production pm2 start <your-main-js-file> --name="<app-name>"
```

- For future deployment you just need to reload to run new code
```bash
pm2 gracefulReload <app-name>
```

# Notes:

- Follow pm2 documentation http://pm2.keymetrics.io/docs/usage/quick-start/
to understand and use all of its commands and advanced features.
- Want to get rid of repetitive tasks? You can automate your deployment, using
pm2 deployment http://pm2.keymetrics.io/docs/usage/deployment/. There will be
a documentation for this.