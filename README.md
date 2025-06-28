# fits-api

[![npm version](https://badge.fury.io/js/fits-api.svg)](https://www.npmjs.com/package/fits-api)  
[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

**fits-api** (Fast Implemented TikTok Scraper API) is an unofficial Node.js SDK that retrieves public TikTok data using scraping techniques and dynamic signature generation with Playwright.

> Developed with ❤️ by [KinglyShade](https://github.com/kinglyfenixstudios) for educational and research purposes.

---

## Installation

To install and set up the API, follow these steps:

1. Install the project dependencies:

```bash
npm install fits-api
````

2. Install the Chromium browser via Playwright:

```bash
npx playwright install chromium
```

> **Requirements**: Node.js version 16 or higher and an internet connection to access TikTok.

---

## Features

* Retrieve public videos from any TikTok user.
* Filter results by hashtags or keywords.
* Extract video statistics: views, likes, comments, shares.
* Retrieve metadata of the audio used in videos.
* Dynamic signature generation to bypass basic bot protection.

---

## Basic Usage

### Method: `getUserVideos(username: string, options?: { filter?: string[] })`

This function allows you to retrieve public videos of a specific TikTok user.

```ts
import { getUserVideos } from 'fits-api';

(async () => {
  const videos = await getUserVideos('example_username', {
    filter: ['fyp', 'humor']  // Optional keyword filter
  });

  console.log(videos);
})();
```

### Example Response

```json
[
  {
    "id": "1234567890",
    "description": "This is a sample video #humor",
    "playCount": 10000,
    "likeCount": 5000,
    "commentCount": 200,
    "shareCount": 100,
    "hashtags": ["#humor"],
    "audio": {
      "id": "987",
      "title": "Viral Song",
      "videoCount": 4321
    }
  }
]
```

---

## Additional Examples

### Get User Profile Information

You can also retrieve information about the user's profile, such as followers, following, and bio.

```ts
import { getUserProfile } from 'fits-api';

(async () => {
  const profile = await getUserProfile('example_username');
  console.log(profile);
})();
```

### Example Response for User Profile

```json
{
  "username": "example_username",
  "followersCount": 1500,
  "followingCount": 200,
  "bio": "This is the bio of the user.",
  "profilePicture": "https://path-to-profile-picture.jpg"
}
```

### Get Trending Hashtags

You can retrieve a list of currently trending hashtags on TikTok.

```ts
import { getTrendingHashtags } from 'fits-api';

(async () => {
  const trendingHashtags = await getTrendingHashtags();
  console.log(trendingHashtags);
})();
```

### Example Response for Trending Hashtags

```json
[
  "#fyp",
  "#viral",
  "#funny",
  "#dance",
  "#trending"
]
```

### Get Video Comments

Retrieve the comments of a specific video by its ID.

```ts
import { getVideoComments } from 'fits-api';

(async () => {
  const comments = await getVideoComments('1234567890');
  console.log(comments);
})();
```

### Example Response for Video Comments

```json
[
  {
    "user": "user1",
    "comment": "This is hilarious!",
    "likeCount": 120
  },
  {
    "user": "user2",
    "comment": "Love this content!",
    "likeCount": 80
  }
]
```

---

## Technical Requirements

* **Node.js** version 16 or higher.
* Project dependencies installed (`npm install`).
* Chromium browser installed via Playwright:

  ```bash
  npx playwright install chromium
  ```

---

## Best Practices

* Use keyword filters to reduce unnecessary requests.
* Avoid large-scale scraping or automation (TikTok may block your IP).
* Ensure that the requested content is public and adheres to TikTok’s terms of service.

---

## Legal Disclaimer

This package is **unofficial** and **not affiliated with TikTok**. The primary purpose of this tool is educational, but we are not responsible for any use for other purposes. TikTok may change its platform at any time, which could break the compatibility of this tool.

**By using this package, you acknowledge that:**

* The use of this API is **at your own risk**, and the developer is not responsible for any damages, losses, or consequences arising from misuse.
* This software is **not open source**.
* The use of this tool must always comply with TikTok's **privacy policies** and **terms of service**.

---

## Author

**KinglyShade**
🔗 [GitHub](https://github.com/kinglyfenixstudios)
📦 [npm](https://www.npmjs.com/package/fits-api)

---

## License

Distributed under the **MIT License**.
See the [LICENSE](./LICENSE) file for details.
