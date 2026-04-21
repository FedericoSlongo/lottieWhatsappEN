# 🧩 Lottie Sticker Builder (WAS) — Beta

Transforms an image (**buffer** or **file**) into an animated `.was` sticker (Lottie) ready to use on WhatsApp.

---

## ⚡ Installation

### 1. Clone or download the project

```bash
git clone https://github.com/Pedrozz13755/Lottie-Whatsapp.git
cd Lottie-Whatsapp
```

Or, if you prefer, just place the files inside your own project.

---

### 2. Install the required dependencies

This code uses only native Node.js modules, but the `zip` command must be installed on the system.

On Linux / Termux / Ubuntu:

```bash
pkg install zip
# or
apt install zip
```

---

## 📦 Expected structure

You need a base folder containing the Lottie files. Example:

```
src/
 └── exemple/
      └── animation/
           └── animation_secondary.json
```

This JSON file must already contain a base64 image inside it, because the builder will automatically replace that image.

---

## 🚀 How to use

### Import the function

```js
const { buildLottieSticker } = require("./src/index");
```

---

### Simple example

```js
const path = require("path");
const { buildLottieSticker } = require("./src/index");

const output = await buildLottieSticker({
  baseFolder: path.resolve(__dirname, "src", "exemple"),
  buffer: dfileBuffer,
  mime: "image/jpeg",
  output: path.resolve(__dirname, "jurubeba.was")
});
```

---

### Send on WhatsApp with Baileys

```js
const fs = require("fs");

await client.sendMessage(from, {
  sticker: fs.readFileSync("./jurubeba.was"),
  mimetype: "application/was"
});
```

---

## 🧠 Parameters

| Name               | Type   | Required | Description                                       |
| ------------------ | ------ | -------- | ------------------------------------------------- |
| `baseFolder`       | string | ✅        | Base Lottie folder                                |
| `buffer`           | Buffer | ❌        | Image in memory                                   |
| `imagePath`        | string | ❌        | Image file path                                   |
| `mime`             | string | ❌        | Image type (auto-detected if you use `imagePath`) |
| `output`           | string | ❌        | Final `.was` file path                            |
| `jsonRelativePath` | string | ❌        | JSON path inside the base folder                  |

---

## ⚠️ Important rules

* You must provide **`buffer` or `imagePath`**
* Supported formats:

  * PNG
  * JPG / JPEG
  * WEBP
* The Lottie JSON must already contain an embedded base64 image
* The code only replaces the existing image; it does not create the Lottie structure from scratch

---

## 💥 Common errors

### `Mime not detected`

You did not provide `mime` or `imagePath`

### `JSON without assets`

The JSON file is invalid or does not contain the expected structure

### `No base64 image found in Lottie`

Your Lottie file does not contain an embedded base64 image to replace

### `zip not found`

The `zip` command is not installed on the system

---

## 🛠️ Useful tip

If you want to use it directly with an image received from WhatsApp, you can grab the buffer and send it to the builder:

```js
const buffer = await getFileBuffer(message, "image");

const output = await buildLottieSticker({
  baseFolder: path.resolve(__dirname, "src", "exemple"),
  buffer,
  mime: "image/jpeg",
  output: path.resolve(__dirname, "jurubeba.was")
});
```

---

## 🚧 Project status

> ⚠️ **BETA VERSION**
>
> This project is still in beta.
> Depending on the Lottie file used, some animations may not work correctly.
> There is still no guaranteed support for all Lottie structure types.

---

## 👑 Credits

Developed by **Pedrozz Mods**

This project is still under development and in beta.
If you use, modify, or share it, keep the credits.

Group: [https://chat.whatsapp.com/C21cogFUmKABh9e3qyexSQ?mode=gi_t](https://chat.whatsapp.com/C21cogFUmKABh9e3qyexSQ?mode=gi_t)
Channel: [https://whatsapp.com/channel/0029Vb8CYiZChq6RIEfS7K1D](https://whatsapp.com/channel/0029Vb8CYiZChq6RIEfS7K1D)

---

### Footer

Made by **Pedrozz Mods**
Project in **beta version**, subject to changes and possible bugs.

