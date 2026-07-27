# AWN Proposal Builder - three deliverables

This bundle contains the Proposal Builder in two forms, plus everything needed to run it as an Outlook add-in. Both new fields (**Consultants involved** and **Project currency €/£**) are included in all versions. Choosing GBP switches the fee symbol to £ and formats the fee in en-GB.

## What is in the box

### 1. `proposal-builder.html` - standalone (mailto)
A single self-contained file. Double-click to open in any browser.
- The **Send to Proposals Team** button opens a pre-filled plain-text email to project@awnconsulting.com via your default mail client (mailto).
- No hosting required. Ideal for quick desktop use or dropping on SharePoint/OneDrive for download.

### 2. `taskpane.html` - the Outlook add-in page (native Office.js)
Same interface, but the button is **Create Outlook email**. When run inside Outlook as an add-in it uses the Office JavaScript API (`displayNewMessageForm`) to open a **fully formatted HTML email** directly in Outlook, with clickable template links, no mailto needed.
- If opened in a plain browser (no Outlook), it automatically falls back to mailto so it still works.

### 3. `manifest.xml` + icons - the add-in definition
`manifest.xml` tells Outlook where the task pane lives and adds a **Proposal Builder** button to the ribbon (both when reading and composing mail). Icons: `addin-icon-16/32/64/80/128.png`.

---

## Deploying the add-in

### Step A: Host the files on HTTPS
The add-in needs `taskpane.html` and the icon PNGs served over `https://`. Any HTTPS location works (GitHub Pages, a web server, etc). Put all files in the same folder.

### Step B: Edit the manifest
Open `manifest.xml` and replace every `https://YOUR-HOST` with your actual hosting URL (there are several). Also generate a fresh GUID for the `<Id>` element (any online GUID generator).

### Step C: Install it
**Just for you / a few people (no admin needed) - sideload:**
1. Go to **https://aka.ms/olksideload** in a browser (opens the "Add-Ins for Outlook" dialog).
2. Select **My add-ins > Custom Addins > Add a custom add-in > Add from file**.
3. Choose your edited `manifest.xml` and select **Install**.
4. The **Proposal Builder** button appears on the Outlook ribbon. Karine and Sinead can each do the same.

**Whole organisation (needs Global/Exchange Admin):**
1. Microsoft 365 admin centre > **Settings > Integrated apps > Deploy Add-in**.
2. **Upload custom apps**, provide the manifest (file or URL), validate, and assign to Everyone or selected users.
3. Allow up to 24 hours to appear for users.

---

## Known limitation on mobile
The template links use Windows Box desktop paths (`C:\Users\...\Box\...`), so they open on Windows desktop only. On phones/tablets they will not resolve. To make templates open on mobile, replace the file paths with **Box or SharePoint web share links**.
