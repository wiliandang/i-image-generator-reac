{
  "name": "ai-image-backend",
  "version": "1.0.0",
  "type": "module",
  "main": "index.js",
  "scripts": {
    "start": "node index.js",
    "dev": "nodemon index.js"
  },
  "dependencies": {
    "axios": "^1.6.8",
    "cors": "^2.8.5",
    "express": "^4.18.2",
    "body-parser": "^1.20.2"
  },
  "devDependencies": {
    "nodemon": "^3.0.1"
  }
}import express from 'express';
import cors from 'cors';
import bodyParser from 'body-parser';

import generateImage from './api/generate-image.js';
import captionImage from './api/caption-image.js';

const app = express();
const PORT = process.env.PORT || 3000;

app.use(cors());
app.use(bodyParser.json());

app.use('/api', generateImage);
app.use('/api', captionImage);

app.get('/', (req, res) => {
  res.send('✅ AI Generator API is running');
});

app.listen(PORT, () => {
  console.log(`🚀 Server berjalan di http://localhost:${PORT}`);
});import express from 'express';
import axios from 'axios';

const router = express.Router();

router.post('/generate-image', async (req, res) => {
  const { prompt, model = 'stability', style = 'realistic', aspectRatio = '1:1' } = req.body;

  try {
    const generatedImages = Array.from({ length: 4 }).map((_, i) => ({
      url: `https://source.unsplash.com/800x600/?${encodeURIComponent(prompt)}&sig=${Math.random()}`,
      meta: {
        prompt,
        model,
        style,
        aspectRatio,
        time: new Date().toISOString(),
      },
    }));

    res.json({ images: generatedImages });
  } catch (err) {
    res.status(500).json({ error: 'Gagal generate gambar', details: err.message });
  }
});

export default router;import express from 'express';

const router = express.Router();

router.post('/caption-image', async (req, res) => {
  const { imageUrl } = req.body;
  const fakeCaption = 'Wanita duduk di sofa dengan pencahayaan alami dan suasana hangat';
  res.json({ caption: fakeCaption, source: imageUrl });
});

export default router;
