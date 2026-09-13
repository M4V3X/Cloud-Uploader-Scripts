# ☁️ Cloud Uploader Scripts

While learning about Red Team operations and researching different techniques, I found that file transfer can be an important part of an engagement.

I noticed that Red Team operations may sometimes need to transfer collected files to an external location. One option is to set up a custom server or build your own infrastructure, but that also means dealing with hosting, domains, SSL certificates, and server management.

Then I started thinking about another option.

There are already legitimate cloud storage platforms that people and organizations use every day, such as Dropbox, Google Drive, and OneDrive. These platforms already provide HTTPS, authentication, APIs, and the infrastructure needed to store files.

So I wanted to explore the idea of building tools that could interact with these platforms using their official APIs instead of building a separate server from scratch.

That's how this project started.

I created separate C++ implementations for Dropbox, Google Drive, and OneDrive. Each one communicates with its platform using the official API and uploads files to a configured cloud storage account.


---

## 💡 How It Works

Each tool starts from the same directory where the executable is located.

From there, it goes through the directory and all subdirectories, finds the files, and uploads them to the configured cloud storage account.

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

The uploader will go through everything inside that directory and process the files it finds.

> ⚠️ Be careful when testing these tools. They can process files recursively from the executable's directory and its subdirectories.

---

## 📦 What's Inside

| File              | Platform     |
| ----------------- | ------------ |
| `Dropbox.cpp`     | Dropbox      |
| `GoogleDrive.cpp` | Google Drive |
| `OneDrive.cpp`    | OneDrive     |

Each file is a separate implementation for a different cloud storage provider.

---

## ⚙️ Requirements

| Requirement          | Details                            |
| -------------------- | ---------------------------------- |
| **Compiler**         | MinGW-w64                          |
| **Access Token**     | Required for the selected platform |

The tools use the Windows WinHTTP library to make HTTPS requests.

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

Before using any of the tools, you need to create your own application and get an access token for the platform you want to test.

### Dropbox

Create an application from the Dropbox App Console and configure the permissions required for file access.

[Dropbox App Console](https://www.dropbox.com/developers/apps?utm_source=chatgpt.com)

---

### Google Drive

Create a project, enable the Google Drive API, and configure OAuth credentials for your application.

[Google Cloud Console](https://console.cloud.google.com/?utm_source=chatgpt.com)

---

### OneDrive

Register an application and configure the required Microsoft Graph permissions.

[Microsoft Azure Portal](https://portal.azure.com/?utm_source=chatgpt.com)

---

## 🛡️ Disclaimer

This project was created for learning, research, Red Team labs, and authorized security testing.

Please only use it on systems, files, and accounts that you own or have explicit permission to test.

I am not responsible for any misuse of this project.
