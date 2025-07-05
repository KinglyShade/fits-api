

# 🎯 FITS-API · Fast Implemented TikTok Scraper API  

[![npm version](https://badge.fury.io/js/fits-api.svg)](https://www.npmjs.com/package/fits-api)  
[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](./LICENSE)  

> ⚠️ **Private SDK** · This package is proprietary and intended for internal/private use only.  
> Not open-source or publicly redistributable.  

---

## 📦 Installation  

Install the package and required dependencies:

```bash
npm install fits-api
npx playwright install chromium
```

**Requirements:**
- Node.js v18 or higher
- Internet connectivity to access TikTok and run Chromium for dynamic signature generation

## ✨ Features  

- 📹 Fetch public videos from any TikTok user profile  
- 👤 Retrieve detailed public profile metadata  
- 🔐 Automatic dynamic signature generation using embedded Chromium via Playwright  
- 🚧 Robust error handling with graceful fallback for invalid or inaccessible users  
- 🧪 Comprehensive Jest tests covering core SDK functionality  

## 🚀 Quick Start  

### Fetch User Videos  

```typescript
import { getUserVideos } from 'fits-api';

async function fetchVideos() {
  const videos = await getUserVideos('tiktok', { limit: 5 });
  console.log('Videos:', videos);
}

fetchVideos();
```

### Fetch User Profile  

```typescript
import { getUserProfile } from 'fits-api';

async function fetchProfile() {
  const profile = await getUserProfile('tiktok');
  console.log('Profile:', profile);
}

fetchProfile();
```

## 🧱 API Reference  

### `getUserVideos(username: string, options?: { limit?: number }): Promise<Video[]>`

- **username**: TikTok username without the `@` prefix  
- **options.limit**: Maximum number of videos to retrieve (default: 10)  

Returns a promise resolving to an array of video objects or an empty array if the user does not exist.  

Each video object includes:  
- `id`: Video ID string  
- `description`: Video description text  
- `playCount`: Number of plays  
- `likeCount`: Number of likes  
- `commentCount`: Number of comments  
- `shareCount`: Number of shares  
- `hashtags`: Array of hashtags extracted from description  
- `audio`: Object with audio details:  
  - `id`: Audio ID  
  - `title`: Audio title  
  - `videoCount`: Number of videos using this audio  

### `getUserProfile(username: string): Promise<UserProfile | null>`

- **username**: TikTok username without the `@` prefix  

Returns a promise resolving to a user profile object or `null` if the profile is not accessible or does not exist.  

Each profile object includes:  
- `username`: User's TikTok handle  
- `followersCount`: Number of followers  
- `followingCount`: Number of accounts followed  
- `bio`: User biography text  
- `profilePicture`: URL to profile picture  
- `totalLikes`: Total likes received  
- `totalVideos`: Total videos posted  
- `verified`: Boolean indicating verified status  
- `location`: User location if available  

## 💡 Real-World Usage Examples  

### 1. Display Top 3 Videos of a User  

```typescript
import { getUserVideos } from 'fits-api';

async function showTopVideos(username: string) {
  const videos = await getUserVideos(username, { limit: 3 });
  videos.forEach((video, index) => {
    console.log(`#${index + 1} - ${video.description}`);
    console.log(`Views: ${video.playCount}, Likes: ${video.likeCount}`);
    console.log(`Audio: ${video.audio.title} (used in ${video.audio.videoCount} videos)`);
    console.log('---');
  });
}

showTopVideos('charlidamelio');
```

### 2. Aggregate Total Likes Across User's Videos  

```typescript
import { getUserVideos } from 'fits-api';

async function totalLikes(username: string) {
  const videos = await getUserVideos(username, { limit: 50 });
  const sumLikes = videos.reduce((acc, video) => acc + video.likeCount, 0);
  console.log(`User @${username} has a total of ${sumLikes} likes across ${videos.length} videos.`);
}

totalLikes('addisonre');
```

### 3. Fetch Profile and Check Verification Status  

```typescript
import { getUserProfile } from 'fits-api';

async function checkVerification(username: string) {
  const profile = await getUserProfile(username);
  if (!profile) {
    console.log(`User @${username} not found or profile is private.`);
    return;
  }
  console.log(`@${username} is ${profile.verified ? 'verified ✅' : 'not verified ❌'}`);
  console.log(`Followers: ${profile.followersCount}`);
  console.log(`Bio: ${profile.bio}`);
}

checkVerification('zachking');
```

### 4. Filter Videos by Hashtag  

```typescript
import { getUserVideos } from 'fits-api';

async function filterVideosByHashtag(username: string, hashtag: string) {
  const videos = await getUserVideos(username, { limit: 20 });
  const filtered = videos.filter(video => video.hashtags.includes(`#${hashtag.toLowerCase()}`));
  console.log(`Videos with hashtag #${hashtag}:`);
  filtered.forEach(video => {
    console.log(`- ${video.description} (Likes: ${video.likeCount})`);
  });
}

filterVideosByHashtag('lorengray', 'dance');
```

### 5. Build a Simple Dashboard Data Fetcher  

```typescript
import { getUserProfile, getUserVideos } from 'fits-api';

async function fetchDashboardData(username: string) {
  const profile = await getUserProfile(username);
  const videos = await getUserVideos(username, { limit: 10 });

  return {
    profile,
    recentVideos: videos.map(v => ({
      id: v.id,
      description: v.description,
      likes: v.likeCount,
      plays: v.playCount,
      audioTitle: v.audio.title
    }))
  };
}

fetchDashboardData('babyariel').then(data => {
  console.log('Dashboard Data:', data);
});
```

## ⚙️ Requirements  

- Node.js v18 or higher  
- Chromium browser installed via Playwright (`npx playwright install chromium`)  
- Server or environment with internet access to reach TikTok  

## 🛠 Build & Publish  

### Build  

```bash
npm run build
```

### Publish to NPM  

```bash
npm version patch  # or minor / major
npm publish
```

> **Note**: Ensure you are logged in with `npm login` before publishing.

## 🗣 Support & Feedback  

This repository serves as the official documentation and issue tracker for `fits-api`.  

While the SDK source code is not open-source, you can:  
- Use GitHub Issues to:  
  - Report bugs  
  - Request new features  
  - Ask usage questions  

> **Note**: Pull requests are not accepted.

## 🔐 Important Usage Notes  

- Relies on headless Chromium to generate TikTok’s required `_signature` parameters dynamically  
- TikTok’s anti-bot measures may change; periodic re-validation and updates may be necessary  
- A JavaScript fallback using JSDOM is included but has limited scraping capabilities compared to Chromium  

## ⚖️ Legal Disclaimer  

This project is not affiliated with TikTok. It is intended solely for:  
- ✅ Educational purposes  
- ✅ Development and testing  
- ✅ Internal data analysis  

By using this SDK, you agree to:  
- Comply with TikTok’s Terms of Service  
- Not redistribute this SDK as open source  
- Assume full responsibility for your use of this software  

## 👤 Author  

**KinglyShade**  
[GitHub](https://github.com/KinglyShade) | [npm](https://www.npmjs.com/~kinglyshade)  

## 📄 License  

MIT License  

Copyright (c) 2025 KinglyShade  

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:  

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.  

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.


