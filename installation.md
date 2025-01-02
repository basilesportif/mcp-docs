# Installing LibreChat with npm and nvm

This guide covers how to install LibreChat locally using npm and nvm (Node Version Manager), including MongoDB setup options.

## Prerequisites

- Git
- MongoDB (local or cloud)
- Terminal access

## Node.js Setup with NVM

1. **Install NVM**

   On macOS and Linux:
   ```bash
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
   ```

   On Windows:
   - Use [nvm-windows](https://github.com/coreybutler/nvm-windows)
   - Download and run the installer from the [latest release](https://github.com/coreybutler/nvm-windows/releases)

2. **Restart your terminal or reload your profile**
   ```bash
   # On macOS/Linux, run one of these depending on your shell:
   source ~/.bashrc
   source ~/.zshrc
   source ~/.profile
   ```

3. **Verify NVM installation**
   ```bash
   nvm --version
   ```

4. **Install Node.js LTS version**
   ```bash
   nvm install --lts
   nvm use --lts
   ```

5. **Verify Node.js and npm installation**
   ```bash
   node --version
   npm --version
   ```

## Installation Steps

1. **Clone the Repository**
```bash
git clone https://github.com/danny-avila/LibreChat.git
cd LibreChat
```

2. **Install Dependencies**
```bash
npm install
```

3. **Create Environment File**
```bash
cp .env.example .env
```

4. **Build the Application**
```bash
npm run build
```

5. **Start the Application**
```bash
npm run start
```

The application should now be running at http://localhost:3080

## MongoDB Setup Options

You have two options for setting up MongoDB: local installation or cloud-hosted (MongoDB Atlas).

### Option 1: Local MongoDB Installation

#### On macOS (using Homebrew):
```bash
# Install MongoDB
brew tap mongodb/brew
brew install mongodb-community

# Start MongoDB service
brew services start mongodb-community
```

#### On Linux (Ubuntu/Debian):
```bash
# Import MongoDB public key
curl -fsSL https://pgp.mongodb.com/server-6.0.asc | \
   sudo gpg -o /usr/share/keyrings/mongodb-server-6.0.gpg \
   --dearmor

# Add MongoDB repository
echo "deb [ arch=amd64,arm64 signed-by=/usr/share/keyrings/mongodb-server-6.0.gpg ] https://repo.mongodb.org/apt/ubuntu jammy/mongodb-org/6.0 multiverse" | \
   sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list

# Update and install
sudo apt-get update
sudo apt-get install -y mongodb-org

# Start MongoDB
sudo systemctl start mongod
sudo systemctl enable mongod
```

#### On Windows:
1. Download MongoDB Community Server from [MongoDB Download Center](https://www.mongodb.com/try/download/community)
2. Run the installer
3. Follow the installation wizard
4. Start MongoDB service from Services or using:
```bash
net start MongoDB
```

After installing MongoDB locally, update your `.env` file with:
```
MONGO_URI=mongodb://localhost:27017/librechat
```

### Option 2: MongoDB Atlas (Cloud Hosted)

1. Go to [MongoDB Atlas](https://account.mongodb.com/account/register)
2. Create a free account
3. Create a new project (e.g., "LibreChat")
4. Create a new cluster (free tier is sufficient)
5. Set up database access:
   - Create a database user
   - Set a secure password
6. Set up network access:
   - Add your IP address
   - Or allow access from anywhere (0.0.0.0/0) for development
7. Get your connection string:
   - Click "Connect"
   - Choose "Connect your application"
   - Copy the connection string

Update your `.env` file with the MongoDB Atlas connection string:
```
MONGO_URI=mongodb+srv://<username>:<password>@cluster0.xxxxx.mongodb.net/librechat?retryWrites=true&w=majority
```
Replace `<username>`, `<password>`, and the cluster details with your actual values.

## Verifying the Installation

1. **Check MongoDB Connection**
```bash
# For local MongoDB
mongosh

# You should see the MongoDB shell
# Type 'exit' to leave the shell
```

2. **Check LibreChat**
- Open http://localhost:3080 in your browser
- Create an account
- Try sending a message

## Troubleshooting

### Node.js and NVM Issues
1. **NVM Command Not Found**
   - Ensure NVM is properly installed
   - Check if NVM path is in your shell profile
   - Try reloading your shell profile or restart terminal

2. **Node Version Switching Failed**
   - Clear NVM cache: `nvm cache clear`
   - Reinstall desired version: `nvm install [version]`
   - Check for version availability: `nvm ls-remote`

3. **npm Global Packages Missing After Node Switch**
   - Reinstall global packages for new version:
     ```bash
     nvm install [version] --reinstall-packages-from=[old-version]
     ```
   - Or use `nvm reinstall-packages` for current version

### MongoDB Issues
1. **Connection Refused**
   - Check if MongoDB service is running
   - Verify connection string in `.env`
   - Check network access settings in MongoDB Atlas

2. **Authentication Failed**
   - Verify username and password in connection string
   - Check database user permissions

### LibreChat Issues
1. **Build Errors**
   - Clear npm cache: `npm cache clean --force`
   - Delete node_modules: `rm -rf node_modules`
   - Reinstall dependencies: `npm install`

2. **Runtime Errors**
   - Check logs: `npm run start`
   - Verify all environment variables are set correctly
   - Ensure MongoDB is running and accessible

## Security Notes

1. Never commit your `.env` file
2. Use strong passwords for MongoDB
3. Restrict network access in production
4. Regularly update dependencies
5. Back up your database regularly

## Development Tips

1. **Node.js Version Management**
   ```bash
   # List installed Node.js versions
   nvm ls
   
   # Install a specific version
   nvm install 18.16.0
   
   # Switch to a specific version
   nvm use 18.16.0
   
   # Set default Node.js version
   nvm alias default 18.16.0
   ```

2. **Local Development**
   ```bash
   # Ensure correct Node.js version
   nvm use --lts
   
   # Start development server
   npm run dev
   ```

3. **Monitor MongoDB**:
```bash
# Local MongoDB monitoring
mongosh
use librechat
show collections
```

3. Reset database:
```bash
# In MongoDB shell
use librechat
db.dropDatabase()
```