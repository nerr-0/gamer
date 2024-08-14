Certainly! Below is a basic implementation of the FIFA Performance Analyzer using Node.js with the Express framework. This example provides APIs to save game data and analyze performance. This code is a starting point and will require additional features and validations based on your needs.

### Project Structure
```
fifa-performance-analyzer/
├── server.js
├── package.json
└── routes/
    ├── gameRoutes.js
    └── analysisRoutes.js
```

### 1. `package.json`
Create a `package.json` file to manage your project dependencies.

```json
{
  "name": "fifa-performance-analyzer",
  "version": "1.0.0",
  "description": "A tool to save and analyze FIFA game data for PlayStation.",
  "main": "server.js",
  "scripts": {
    "start": "node server.js"
  },
  "dependencies": {
    "express": "^4.17.3",
    "body-parser": "^1.19.0",
    "fs-extra": "^11.1.0"  // For file operations
  }
}
```

Run `npm install` to install the dependencies.

### 2. `server.js`
This is the entry point of your application where you set up the Express server.

```javascript
const express = require('express');
const bodyParser = require('body-parser');
const fs = require('fs-extra');
const path = require('path');

const app = express();
const port = 3000;

app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));

// Import routes
const gameRoutes = require('./routes/gameRoutes');
const analysisRoutes = require('./routes/analysisRoutes');

// Use routes
app.use('/api/games', gameRoutes);
app.use('/api/analysis', analysisRoutes);

// Start the server
app.listen(port, () => {
  console.log(`Server running at http://localhost:${port}`);
});
```

### 3. `routes/gameRoutes.js`
This route handles saving game data.

```javascript
const express = require('express');
const router = express.Router();
const fs = require('fs-extra');
const path = require('path');

const dataDir = path.join(__dirname, '../data');

// Ensure data directory exists
fs.ensureDirSync(dataDir);

router.post('/save', (req, res) => {
  const { gameId, gameData } = req.body;

  if (!gameId || !gameData) {
    return res.status(400).json({ error: 'gameId and gameData are required' });
  }

  const filePath = path.join(dataDir, `${gameId}.json`);

  fs.writeJson(filePath, gameData, { spaces: 2 })
    .then(() => res.status(200).json({ message: 'Game data saved successfully' }))
    .catch(err => res.status(500).json({ error: 'Failed to save game data', details: err }));
});

module.exports = router;
```

### 4. `routes/analysisRoutes.js`
This route handles analyzing saved game data.

```javascript
const express = require('express');
const router = express.Router();
const fs = require('fs-extra');
const path = require('path');

const dataDir = path.join(__dirname, '../data');

router.get('/performance/:gameId', async (req, res) => {
  const { gameId } = req.params;
  const filePath = path.join(dataDir, `${gameId}.json`);

  try {
    const gameData = await fs.readJson(filePath);
    // Example analysis - you can customize this
    const performance = {
      goals: gameData.goals || 0,
      assists: gameData.assists || 0,
      possession: gameData.possession || 0
    };

    res.status(200).json(performance);
  } catch (err) {
    res.status(404).json({ error: 'Game data not found', details: err });
  }
});

module.exports = router;
```

### Notes

1. **Error Handling**: This example provides basic error handling. You might want to expand on this for production use.
2. **Data Validation**: Make sure to validate and sanitize your inputs to avoid issues related to malformed data.
3. **Security**: Consider implementing security measures such as authentication and authorization if the tool is to be used by multiple users.
4. **Testing**: Add tests to ensure your APIs work as expected. 

This setup provides a simple backend to save and analyze FIFA game data using Node.js and Express. Adjust the analysis logic according to your specific needs.
