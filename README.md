<h1 align="center">☁️ Cloud Uploader Scripts</h1>

While learning about Red Team stuff, I came across the idea that file transfer is something you may need during an engagement.

At first, I thought about the usual way of doing it — setting up a server, getting a domain, configuring SSL, and dealing with all the extra infrastructure.

Then I thought, why build all of that when platforms like Dropbox, Google Drive, and OneDrive already exist and provide APIs for uploading files?

So I decided to experiment with the idea and built a few C++ tools that use the official APIs of these platforms to upload files to my own cloud storage

---

## 💡 How It Works

Once you run the `.exe`, it starts from the same folder where the executable is located.

It goes through the folder and all its subfolders, finds the files there, and starts uploading them to the configured cloud storage.

For example:

```text
Uploader.exe
├── file1.txt
├── file2.pdf
│
└── Folder
    ├── image.png
    └── data.txt
```

So basically, you just run the `.exe`, and it automatically goes through everything inside that folder and starts uploading the files.

> [!WARNING]
> Running the `.exe` automatically processes files in its folder and all subfolders. Make sure you're running it in the right directory.
---

## 🚀 Compilation

### Dropbox

```bash
x86_64-w64-mingw32-g++ Dropbox.cpp -o Dropbox.exe -std=c++17 -lwinhttp -static-libgcc -static-libstdc++ -mwindows
```

### Google Drive

```bash
x86_64-w64-mingw32-g++ GoogleDrive.cpp -o GoogleDrive.exe -std=c++17 -lwinhttp -static-libgcc -static-libstdc++ -mwindows
```

### OneDrive

```bash
x86_64-w64-mingw32-g++ OneDrive.cpp -o OneDrive.exe -std=c++17 -lwinhttp -static-libgcc -static-libstdc++ -mwindows
```

I used `-mwindows` so the executable runs without opening a console window.

---

## 🔑 Access Tokens

Each tool needs an access token with the required permissions for uploading files to the selected cloud platform.

### Dropbox

The token needs permission to upload and manage files:

- `files.content.write`
- `files.content.read`

![Dropbox Access Token](images/dropbox-token.png)

---

### Google Drive

The token needs access to Google Drive:

- `https://www.googleapis.com/auth/drive`

![Google Drive Access Token](images/google-drive-token.png)

---

### OneDrive

The token needs permission to read and write files:

- `Files.ReadWrite.All`
- `User.Read`

![OneDrive Access Token](images/onedrive-token.png)

---

> [!WARNING]
> This project is for learning, research, Red Team labs, and authorized security testing only.
>
> Only use it on systems, files, and accounts you own or have permission to test.
