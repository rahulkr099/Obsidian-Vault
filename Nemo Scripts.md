Sure Rahul! Here are some **super useful Nemo scripts** for a MERN + Python + Linux user like you. These will show up under:

👉 **Right-click → Scripts**

Just create the file inside:

```
~/.local/share/nemo/scripts/
```

Make it executable:

```
chmod +x scriptname.sh
```

I’ll give you **simple**, **developer-friendly**, and **error-free** scripts.

---

# 🌟 **1. Open Terminal in Folder**

(Works for both files and folders)

```bash
#!/bin/bash
gnome-terminal --working-directory="$(dirname "$1")"
```

✔ Opens terminal in correct directory  
✔ Very useful for coding

---

# 🌟 **2. Run Python File (DSA Helper)**

```bash
#!/bin/bash

file="$1"

if [[ "$file" == *.py ]]; then
    gnome-terminal -- bash -c "python3 \"$file\"; exec bash"
else
    notify-send "Not a Python file" "Select a .py file to run."
fi
```

✔ Right-click any `.py` → instantly runs  
✔ Good for quick practice

---

# 🌟 **3. Start a MERN Project (Frontend + Backend)**

```bash
#!/bin/bash

project_dir="$(dirname "$1")"

gnome-terminal --working-directory="$project_dir/server" -- bash -c "npm start; exec bash"
gnome-terminal --working-directory="$project_dir/client" -- bash -c "npm start; exec bash"
```

✔ Opens two terminals  
✔ Runs frontend & backend automatically  
✔ Boost for MERN workflow

---

# 🌟 **4. Convert Image to WebP (Great for Web Dev)**

```bash
#!/bin/bash

file="$1"
output="${file%.*}.webp"

convert "$file" "$output"
notify-send "Converted to WebP" "$output created."
```

⚠ Requires:

```
sudo apt install imagemagick
```

✔ Perfect for compressing images for your projects

---

# 🌟 **5. Create Express App in One Click**

Right-click empty folder → run script.

```bash
#!/bin/bash

dir="$1"

gnome-terminal --working-directory="$dir" -- bash -c "
npm init -y &&
npm install express cors &&
echo \"const express = require('express');
const app = express();
app.get('/', (req, res) => res.send('Hello World'));
app.listen(3000, () => console.log('Server running on 3000'));
\" > index.js
exec bash
"
```

✔ Auto-creates Express boilerplate  
✔ Saves time in hackathons

---

# 🌟 **6. Compress Folder to ZIP**

```bash
#!/bin/bash

folder="$1"
zipname="${folder##*/}.zip"

zip -r "$zipname" "$folder"
notify-send "ZIP Created" "$zipname saved."
```

✔ Useful for sending projects to friends or GitHub releases

---

# 🌟 **7. Copy File Path (Super handy!)**

```bash
#!/bin/bash

file="$1"
echo -n "$file" | xclip -selection clipboard
notify-send "Copied Path" "$file"
```

✔ Copies full path to clipboard  
✔ Very useful when working with VS Code / config files

Requires:

```
sudo apt install xclip
```

---

# 🌟 If you want, I can make scripts like:

- 🏷 Rename all files with pattern
    
- 🌈 Color folders with script
    
- 🗂 Create MERN boilerplate structure
    
- 🚀 Deploy project to GitHub in one click
    
- 📦 Backup your coding folder automatically
    
- 🎧 Convert audio/video formats
    
- 🧹 Cleanup node_modules automatically
    

Just tell me what you want, and I’ll build perfect Nemo scripts for your workflow.