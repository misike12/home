[简体中文](./README.md) | English

<p>
<strong><h2>Unnamed Homepage</h2></strong>
A simple little homepage, I've seen enough of the original, so I made a new one.
</p>

![Unnamed Homepage](/screenshots/main.jpg)

> The logo font of the homepage has been compressed. If you use letters other than the logo of this site, it will revert to the default font. Here is the [complete font](https://file.imsyy.top/font/Other/Pacifico-Regular.ttf). If you can't download it, you can replace it with `Pacifico-Regular-all.ttf` in the font directory.

### 👀 Demo

> Due to CDN caching, viewing the latest effects may require `Ctrl` + `F5` to force refresh the browser cache.

- [Unnamed Homepage](https://www.imsyy.top)
- [Unnamed Homepage - Dev](https://home-imsyy.vercel.app)
- [Unnamed Homepage - Backup](https://home-5iw.pages.dev)

### 🎉 Features

- [x] Loading animation
- [x] Site introduction
- [x] Hitokoto
- [x] Date and time
- [x] Real-time weather
- [x] Time progress bar
- [x] Music player
- [x] Mobile adaptation

### ⚙️ Automatic Deployment

If there are any errors in the build environment or packaging process, you can use `Github Actions` for automatic building.

- After successfully forking the repository, go to the `Actions` page. If you are opening it for the first time, you will see the prompt below. Click on it to enable it.

  ![Step 1](/screenshots/step1.jpg)

- Then, any modifications made in the repository will trigger the workflow to run. After the workflow is completed, a compressed package will be generated below, which is the built static file. You can upload it to the server by yourself.

  ![Step 2](/screenshots/step2.jpg)

### ⚙️ Manual Deployment

- **Install** [node.js](https://nodejs.org/en/) **environment**

  > node > 16.16.0  
  > npm > 8.15.0

- Then, run the `cmd` terminal as **administrator**, and `cd` to the root directory of the project.
- Enter the following in the `terminal`:

```bash
# Install pnpm
npm install -g pnpm

# Install dependencies
pnpm install

# Preview
pnpm dev

# Build
pnpm build
```

> After the build is completed, the static resources will be generated in the **`dist` directory**. You can upload the files **under the `dist` folder** to the server, or use platforms like `Vercel` to import and deploy automatically.

### ⚙️ Docker Deployment

> Installation and configuration of Docker will not be explained here. Please solve it by yourself.

```bash
# Build
docker build -t home .
# Run
docker run -p 12445:12445 -d home
```

### ⚙️ Vercel Deployment

> Other deployment platforms are similar and will not be explained here.

1. Click `Fork` in the upper right corner of this repository to copy it to your `GitHub` account.
2. Copy the `/.env.example` file and rename it to `/.env` (important).
3. Modify the configuration in the `/.env` file as needed.
4. Click `Deploy` to successfully deploy.

### Website Links

You can customize the website links (to point to your own website) in `src/assets/siteLinks.json`:

```json
{
  "icon": "Blog",
  "name": "Blog",
  "link": "https://blog.imsyy.top/"
},
```

The icon for website links can be added in `src/components/Links/index.vue`:

```js
// You can go to https://www.xicons.org to select and import icons here
// The imported type here is fa
import {
  Link,
  Blog,
  CompactDisc,
  Cloud,
  Compass,
  Book,
  Fire,
  LaptopCode,
} from "@vicons/fa";

...

// Website link icons
const siteIcon = {
  Blog,
  Cloud,
  CompactDisc,
  Compass,
  Book,
  Fire,
  LaptopCode,
};
```

### Social Links

You can customize the social links in `src/assets/socialLinks.json`.

### Weather

To obtain weather and location information, you need to use the related APIs from `Amap Open Platform`.

- Go to [Amap Open Platform Console](https://console.amap.com/dev/index) to create a `Web Service` type `Key`, and fill in the `Key` in `.env` as `VITE_WEATHER_KEY`.

You can also use other methods to obtain weather information.

### Music

> This project uses the `Aplayer` music player based on `MetingJS`, which can quickly customize playlists.
> *Only supports **China Mainland**.

You can change the song-related parameters in the `.env` file to customize the playlist:

```bash
# Song API address
VITE_SONG_API = "https://api-meting.imsyy.top"
# Song server (netease-NetEase Cloud Music, tencent-QQ Music)
VITE_SONG_SERVER = "netease"
# Play type (song-song, playlist-playlist, album-album, search-search, artist-artist)
VITE_SONG_TYPE = "playlist"
# Play ID
VITE_SONG_ID = "7452421335"
```

### Fonts

Currently using the open source font `HarmonyOS Sans`, using font splitting to improve loading speed.

> Since the `CDN` of this site has enabled anti-leeching, **non-site domain names cannot be accessed**. Please change the font import link to the following content, otherwise **custom fonts will not work**.
>
> `https://s1.hdslb.com/bfs/static/jinkela/long/font/regular.css`

<details>
<summary>Old method</summary>

> Since this project introduces Chinese fonts, the Chinese fonts need to be compressed to improve the loading speed of the webpage (you can also cancel the use of Chinese fonts).

#### Remove Traditional Chinese from Chinese Fonts

- Install `Python 3.7` and `pip`
- Run `pip install fonttools`
- Download [sc_unicode.txt](https://gist.githubusercontent.com/imaegoo/d64e5088b723c2e02c40985f55ff12db/raw/5ebd2ce49418c73459a9dfe050483409306a6c1d/sc_unicode.txt)
- Run `pyftsubset fontname.ttf --unicodes-file=sc_unicode.txt`

#### Further Compress Fonts

- Compile and install `Google woff2`

```bash
sudo apt-get install -y git g++ make
git clone --recursive https://github.com/google/woff2.git
cd woff2
make clean all
```

- Compress the font again

```bash
./woff2_compress fontname.ttf
```

- Finally, you can cache the original font and **preload the compressed font**.

> For more information, please visit [虹墨空间站](https://www.imaegoo.com/2020/chinese-font-compress/) for the original article.

</details>

### Website Icon and Background

#### Website Background

You can modify the website background in `public/images`.

If you want to add more local images as website backgrounds, you can rename the images in the form of `background+number`, and modify them in `src/components/Background/index.vue`:

```js
if (type == 0) {
  // Modify the first number after Math.random() here to the number of images
  bgUrl.value = `/images/background${Math.floor(Math.random() * 10 + 1)}.webp`;
}
```

#### Website Icon

You can modify the website icon in `public/images/icon`.

### Tech Stack

- [Vue](https://vuejs.org/)
- [Vite](https://vitejs.dev/)
- [Pinia](https://pinia.esm.dev/)
- [IconPark](https://iconpark.oceanengine.com/official)
- [xicons](https://xicons.org/)
- [Aplayer](https://aplayer.js.org/)

### API

- [Han Xiao Han WebAPI](https://api.vvhan.com/)
- [Bo Tian API](https://api.btstu.cn/doc/sjbz.php)
- [Jiao Shu Xian Sheng API](https://api.oioweb.cn/doc/weather/GetWeather)
- [Amap Open Platform](https://lbs.amap.com/)
- [Hitokoto](https://hitokoto.cn/)

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=imsyy/home&type=Date)](https://star-history.com/#imsyy/home&Date)

<a title="SSL" target="_blank" href="https://myssl.com/seal/detail?domain=blog.imsyy.top"><img src="https://img.shields.io/badge/MySSL-Security%20Certification-brightgreen"></a>&nbsp;<a title="CDN" target="_blank" href="https://cdnjs.com/"><img src="https://img.shields.io/badge/CDN-Cloudflare-blue"></a>&nbsp;<a title="Copyright" target="_blank" href="https://imsyy.top/"><img src="https://img.shields.io/badge/Copyright%20%C2%A9%202020--2023-%E7%84%A1%E5%90%8D-red"></a>
