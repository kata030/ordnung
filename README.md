# Ordnung

### 👉 [Open Ordnung: kata030.github.io/ordnung](https://kata030.github.io/ordnung/)

**Your Firefox bookmarks, sorted into tidy folders by an AI that runs entirely in your browser.**

Years of bookmarks piled up in random folders? Ordnung reads a Firefox bookmark backup, lets a local language model work out sensible topics and a clean folder structure, sorts every bookmark into it, and gives you a new backup file to restore. No account, no server, no upload: your bookmarks never leave your computer.

Available in English and German.

---

## Features

- **100 % local and private.** The language model runs on your own graphics card via WebGPU. Only the model itself is downloaded once from the internet; your bookmarks stay on your machine.
- **A fresh structure, or your own.** Let the model design new top-level folders and subfolders, or keep an existing folder's subfolders and only redistribute the bookmarks across them.
- **Tell it what you want.** Add requests in plain language, such as *"Keep work and personal separate"* or *"Sort recipes by cuisine"*.
- **Merges duplicates.** Bookmarks with the same address are combined into one, keeping their tags and keywords.
- **Combine several backups.** Load more than one backup file (for example from different computers) and sort them together.
- **Review before you commit.** Preview the new structure, drag bookmarks and folders around, rename, create or move folders, then download.
- **Pause and resume.** Progress is saved in the browser, so you can stop the analysis and continue later, even after a reload.
- **Built-in graphics test.** Checks whether your graphics card and driver can handle the model before the long run starts.
- **Fine-tuning.** Set the maximum number of top-level folders, dissolve tiny folders, split overly large ones, and adjust how gently the graphics card is loaded.

## How it works

1. **Load your backup.** Drag in a Firefox bookmark backup (`.json`, or `.jsonlz4` from your profile's `bookmarkbackups` folder).
2. **Choose what to sort.** Bookmarks Menu, Bookmarks Toolbar, Other Bookmarks, Mobile Bookmarks, or a single folder.
3. **Pick a model and start.** Ordnung goes through four phases: *collect topics → design the folder structure → sort the bookmarks → polish* (merging duplicate folders and splitting large ones).
4. **Review and download.** Adjust the result by hand if you like, then download the sorted backup file.
5. **Restore it in Firefox.** Open *Manage Bookmarks* (`Ctrl+Shift+O`) → *Import and Backup* → *Restore* → *Choose File…* and select the downloaded file.

> ⚠️ **Restoring replaces all of your current bookmarks** with the contents of the file. The file therefore also contains everything you didn't sort. Make a fresh backup first to be safe. If you use Firefox Sync, the new structure will reach your other devices as well.

### Creating a backup

In Firefox, open *Manage Bookmarks* (`Ctrl+Shift+O`) → *Import and Backup* → *Backup…* and save the `.json` file. Firefox also keeps automatic daily backups as `.jsonlz4` files in the `bookmarkbackups` folder of your profile (find your profile via `about:profiles`).

## Requirements

- **Firefox with WebGPU.** Ordnung checks this on startup and tells you if WebGPU isn't available.
- **A graphics card with enough memory** for the model you choose:

| Model | Notes | Approx. GPU memory |
|---|---|---|
| Qwen3 8B | best folders, slower | 5.7–6.9 GB |
| Qwen2.5 7B | | 5.1–5.9 GB |
| Llama 3.1 8B | | 5.0–6.1 GB |
| Qwen3 4B | good compromise | 3.4–4.3 GB |
| Qwen3 1.7B | for weaker graphics cards | 2.0–2.6 GB |

The lower figure applies to graphics cards that support 16-bit shaders (`shader-f16`); Ordnung picks the right variant automatically. The model is downloaded on first use (several gigabytes) and cached in the browser, so later runs start much faster.

## Running it yourself

Ordnung is a static web page with no build step. To host your own copy, put these files in the same folder on any web server:

```
index.html
app.js
```

Opening the HTML file directly from your disk (`file://`) may not work fully, because Firefox gives local files limited storage and the model can't be cached. In that case, start a simple local server in the folder, for example:

```
python3 -m http.server
```

and open `http://localhost:8000`.

## Credits

- [WebLLM](https://github.com/mlc-ai/web-llm) by the MLC AI team (Apache License 2.0) runs the language models in the browser. It is loaded from the [jsDelivr](https://www.jsdelivr.com/) CDN at a pinned version.
- The models ([Qwen](https://huggingface.co/Qwen), [Llama](https://www.llama.com/)) are downloaded from Hugging Face and are subject to their own licenses.
