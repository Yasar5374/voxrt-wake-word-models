# 🎙️ voxrt-wake-word-models - Add custom voice commands to devices

[![Download Models](https://img.shields.io/badge/Download-Models-blue.svg)](https://github.com/Yasar5374/voxrt-wake-word-models)

## 📋 What this project does

This project contains small, secure files that help your devices recognize your custom wake words. A wake word is the short phrase you speak to wake up your voice assistant or smart device. 

These files use a format called .vxrt. Each file stays small at about 100 KB. We encrypt these files using a standard called AES-GCM to keep your data safe. You can use these files with the VoxRT software on Android, iOS, and other platforms.

## 🛠️ System requirements

To use these model files, your computer needs the following:

- Windows 10 or Windows 11.
- The VoxRT software installed on your device.
- A working microphone to test your custom phrases.
- An internet connection to download the initial files.

## 📥 How to get the files

You need to download the model files from our repository page. Follow these steps to obtain the correct data for your software:

1. Visit the repository page here: [https://github.com/Yasar5374/voxrt-wake-word-models](https://github.com/Yasar5374/voxrt-wake-word-models).
2. Look for the green button labeled "Code" near the top right of the page.
3. Click the button and select "Download ZIP".
4. Choose a folder on your Windows computer where you wish to save the file.
5. Once the download finishes, navigate to your Downloads folder.
6. Right-click the folder and select "Extract All" to see the individual .vxrt files.

## ⚙️ Setting up the software

After you download the files, you must load them into the VoxRT runtime.

1. Open the VoxRT application on your Windows machine.
2. Navigate to the settings menu inside the app.
3. Select the option labeled "Manage Wake Word Models".
4. Click the "Add New Model" button.
5. Point the file browser to the folder where you extracted the .vxrt files.
6. Select the model file matching the phrase you wish to use.
7. Click "Open" to load the model into your software.

## 🗣️ Using your wake word

Once you load the model, the software begins listening for your phrase. You should test the setup to ensure the microphone hears you clearly. 

1. Speak your chosen wake word clearly into your microphone after loading the model.
2. Watch the status indicator in the VoxRT app.
3. If the indicator lights up, the software detected your voice correctly.
4. If the software does not respond, ensure your microphone has permission to access the application in your Windows Privacy Settings.
5. Adjust the microphone volume if the detection feels inconsistent.

## 🔒 Security and privacy

Your voice data stays on your device. We use strong encryption methods to protect the model files. Because the files are small, they run quickly without slowing down your computer. We do not transmit your voice recordings to any outside servers. Everything happens locally on your machine.

## 💡 Finding more phrases

If you want a specific phrase that you do not see in the current list, visit our main website at voxrt.com. You can request custom models or view the library of available phrases there. Our team updates the repository files regularly as we add support for new languages and specific phrases. Check the repository page occasionally to see if new files exist for your specific device model.

## 🔧 Troubleshooting common problems

Sometimes the software may fail to load a model. Follow these steps to fix the issue:

- Check your file path: Ensure the folder name does not contain special characters which might confuse the software.
- Restart the application: Close the VoxRT app and reopen it after adding a new file.
- Verify file type: Ensure the file ends in .vxrt. Other file types will not work with the system.
- Check microphone access: Go to Windows Settings, then Privacy, then Microphone. Ensure "Allow desktop apps to access your microphone" is set to "On".

## 📦 Understanding the file format

The .vxrt format works specifically with the VoxRT runtime. It contains specialized weight data that tells the software how to interpret speech patterns. You cannot open these files in typical text editors or media players. They function only as inputs for the voice recognition engine. By keeping the files under 100 KB, we ensure that they load into memory instantly, providing a fast response time when you say your wake word.

## 🚀 Future updates

We plan to add more models for different accents and languages. If you have specific needs for a wake word, please contact the development team through the VoxRT website. We track requests to prioritize which phrases we build next. Remember to check back on this GitHub page for the latest model releases. We package all new files into the repository format for easy access. Follow the same download steps outlined above whenever you want to add a fresh model to your collection.