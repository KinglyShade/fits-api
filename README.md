# 🎯 FITS-API · Fast Implemented TikTok Scraper API

[![npm version](https://badge.fury.io/js/fits-api.svg)](https://www.npmjs.com/package/fits-api)
[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg)](./LICENSE)

> ⚠️ **Private SDK** · This package is not open-source and is intended for internal/private use only.

**FITS-API** is an advanced, unofficial Node.js SDK for scraping **public TikTok data** using dynamic signature generation via Playwright (Chromium). It's designed for high-reliability environments like dashboards, reporting tools, or analytics platforms.

---

## 📦 Installation

```bash
npm install fits-api
npx playwright install chromium
````

> ✅ Requires **Node.js v18+** and internet access to reach TikTok and load the required dynamic signature environment.

---

## ✨ Features

* 📹 Fetch public videos from any TikTok profile.
* 👤 Retrieve basic public profile data.
* 🔐 Automatic signature generation using embedded Chromium.
* 🚧 Graceful fallback for invalid or inaccessible users (returns empty data instead of crashing).
* 🧪 Includes working Jest tests for key SDK behaviors.

---

## 🚀 Quick Start

### 🔹 Get User Videos

```ts
import { getUserVideos } from 'fits-api';

const videos = await getUserVideos('tiktok', {
  limit: 3
});

console.log(videos);
```

Returns an array of video metadata or an empty array if the user is not found.

### 🔹 Get User Profile

```ts
import { getUserProfile } from 'fits-api';

const profile = await getUserProfile('tiktok');

console.log(profile);
```

Returns the profile's public metadata (or `null` if not found).

---

## 🧪 Example Test Output

This package includes Jest-based tests:

```bash
npm run tests
```

Sample output:

```
PASS  src/__tests__/user.test.ts
  getUserVideos
    ✓ should fetch user videos with valid username
    ✓ should return empty array for non-existent username
```

> Tests are designed to avoid crashing when TikTok changes structure or rate-limits a user.

---

## 🧱 API Reference

### `getUserVideos(username: string, options?: { limit?: number }): Promise<Video[]>`

* `username`: TikTok username (without `@`)
* `options.limit`: Max number of videos to fetch (default: 10)

Returns: Array of videos or empty array if user not found.

---

### `getUserProfile(username: string): Promise<UserProfile | null>`

Returns: Profile object with fields:

* `username`
* `followersCount`
* `followingCount`
* `bio`
* `profilePicture`

Returns `null` if the user is not accessible.

---

## ⚙️ Requirements

* Node.js **v18+**
* Chromium via `playwright` (`npx playwright install chromium`)
* Server with internet access (e.g. VPS, Docker, etc.)

---

## 🛠 Build & Publish

### Build

```bash
npm run build
```

### Publish to NPM

```bash
npm version patch # or minor / major
npm publish
```

> Ensure you're logged in with `npm login`.
---

## 🗣 Feedback & Support

This repository serves as a **public documentation and issue tracker** for `fits-api`.

Although the source code is **not open-source**, you are welcome to:

- Use the [GitHub Issues](https://github.com/KinglyShade/fits-api/issues) section to:
  - Report bugs
  - Request features
  - Ask usage-related questions

🛑 Pull requests are **not accepted**.


---

## 🔐 Usage Notes

* ❗ This SDK uses **headless Chromium** to generate TikTok’s required `_signature` values.
* 📉 If TikTok changes their anti-bot measures, re-testing may be necessary.
* 🧱 JS fallback (`JSDOM`) is used if Chromium fails (but is limited in capabilities).

---

## ⚖️ Legal Disclaimer

This project is **not affiliated with TikTok**.

It is intended only for:

* ✅ Educational
* ✅ Development
* ✅ Internal analysis

You agree to:

* Not use this SDK to violate TikTok’s [Terms of Service](https://www.tiktok.com/legal/terms-of-service).
* Not redistribute this SDK as open source.
* Assume full responsibility for its use.

---

## 👤 Author

**KinglyShade**
[GitHub](https://github.com/kinglyfenixstudios) • [npm](https://www.npmjs.com/package/fits-api)

---

## 📄 License

MIT License.
See the [LICENSE](./LICENSE) file for full details.


