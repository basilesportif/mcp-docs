# Installing LibreChat with npm

This guide covers how to install LibreChat locally using npm, including MongoDB setup options.

## Prerequisites

- Node.js (Latest LTS version recommended)
- Git
- npm
- MongoDB (local or cloud)

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

1. For local development, use:
```bash
npm run dev
```

2. Monitor MongoDB:
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