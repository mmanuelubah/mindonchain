# MindOnChain Admin Guide

## 1. How to Set and Change Passwords

The passwords for gated content are managed centrally in your `hugo.toml` configuration file. The actual password text is **never** stored; instead, a secure SHA-256 hash of the password is saved.

### To change the password

1. Open `hugo.toml` in your editor.
2. Scroll down to the `[params.passwords]` section. You will see:

   ```toml
   [params.passwords]
   default = "8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92" # Example hash
   ```

3. Generate a new SHA-256 hash for your new password. You can do this in your terminal by running:

   ```bash
   echo -n "MyNewPassword123" | sha256sum
   ```

   *(Alternatively, you can use any free online SHA-256 hash generator).*
4. Replace the old hash string in `hugo.toml` with the new hash.

### To create multiple different passwords

If you want different guides to have different passwords, you can add more keys to `hugo.toml`:

```toml
[params.passwords]
default = "<hash1>"
vip_access = "<hash2>"
```

Then, in the front matter of your post, specify which password to use:

```yaml
password_id: "vip_access"
```

---

## 2. Using Templates for Normal Posts

Normal posts live in the `content/posts/` folder. To create a new post, you need standard Hugo front matter at the top of the Markdown file.

### Standard Public Post Template

```markdown
---
title: "Title of Your Post"
date: 2026-08-08
draft: false
tags: ["updates", "news"]
---

Write your post content here...
```

### Password-Protected Post Template

To make **any** post password-protected, just add `private: true`.

```markdown
---
title: "Secret Post"
date: 2026-08-08
draft: false
private: true
password_id: "default"
---

This content will be hidden behind the elegant password gate!
```

---

## 3. Creating and Using Templates in Obsidian

Since you write your content in Obsidian, you can use Obsidian's core **Templates** feature to generate these files instantly.

### Step A: Setup the Templates Folder

1. Open Obsidian and create a new folder named `Templates` (if you don't already have one).
2. Go to **Settings > Core Plugins > Templates** and enable it.
3. Click the gear icon next to Templates and set the **Template folder location** to your `Templates` folder.

### Step B: Create the Guide Template

1. Create a new note inside the `Templates` folder. Name it `Gated Guide Template`.
2. Paste the following text into the note:

   ```markdown
   ---
   title: "{{title}}"
   date: {{date}}
   draft: true
   private: true
   password_id: "default"
   tags: []
   ---

   # Introduction

   Write the guide content here...
   ```

### Step C: Use the Template

1. When you are ready to write a new guide, create a new note in Obsidian (inside `content/alltech/` or `content/programming/`).
2. Press `Ctrl + P` (or `Cmd + P` on Mac) to open the command palette.
3. Type **Insert template** and press Enter.
4. Select `Gated Guide Template`.
5. Obsidian will automatically fill in the front matter, the current date, and set `private: true` so it is instantly protected on your website!

## 4. Setting Up Frontmatter Templates (For ECU Database & Guides)

To standardize your newly merged `alltech/database` section, you should create additional Obsidian templates.

### Template: `ECU Database & Guide`

Use this when manually adding a new ECU pinout, OBD procedure, or immobilizer guide to the Database.

```markdown
---
title: "{{title}}"
date: {{date}}
draft: false
tags: ["bench", "eeprom"]
categories: ["Database", "Immobilizer"]
brand: "Brand Name"
model: "Car Model"
ecu: "ECU Part Number"
---

## 🚗 Vehicle Details
| Field | Value |
|-------|-------|
| **Brand** | Brand Name |
| **Model** | Car Model |
| **Year** | Year Range |

---

## 🔌 ECU Details
| Field | Value |
|-------|-------|
| **Manufacturer** | ECU Maker |
| **ECU Number** | ECU Part Number |

---

## 🔧 Programming Instructions
**Method:** `BENCH`

1. First step goes here...
2. Second step goes here...

---

## 🖼️ Pinout Diagram
![Pinout Diagram](https://drive.google.com/uc?export=view&id=YOUR_FILE_ID)
```

## 5. Linking Images and PDFs from Google Drive

To keep the website incredibly fast and save storage, **all images and PDFs will be hosted on your Google Drive**.

### Step 1: Organize Your Google Drive

When you share the folder with the nested car brands, organize it clearly:

- `Locksmith_Database/`
  - `Toyota/`
    - `Camry_2016_Pinout.jpg`

### Step 2: Get the Google Drive Link

1. Right-click the image or PDF in Google Drive and select **Share**.
2. Change the access from "Restricted" to **"Anyone with the link"**.
3. Click **"Copy Link"**.
   - The link will look like this: `https://drive.google.com/file/d/1a2b3c4d5e6f7g8h9i/view?usp=sharing`

### Step 3: Convert the Link for Your Website

Hugo needs a direct download link to display the image. You must take the **FILE ID** from the link above (e.g., `1a2b3c4d5e6f7g8h9i`) and format it like this:

**`https://drive.google.com/uc?export=view&id=YOUR_FILE_ID`**

### Step 4: Add it to Your Obsidian Post

- **For an Image inside the text:**
  `![Image Description](https://drive.google.com/uc?export=view&id=YOUR_FILE_ID)`
- **For a PDF Download Link:**
  `[Click Here to Download PDF Manual](https://drive.google.com/uc?export=download&id=YOUR_FILE_ID)`
- **For a Cover Image (in the Frontmatter):**
  Just paste the converted link inside the quotes for `images:` or `cover:`.
