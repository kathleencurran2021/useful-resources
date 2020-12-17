# useful-resources
This repo has code snippets, directions, resources, etc, to use as a reference


1. Ionic 
2. React






# Ionic 
## Mobile Dev Environment Setup
1. Turn on Hidden folders 
    1. In terminal run $ defaults write com.apple.finder AppleShowAllFiles YES
2. Make sure you have Catalina installed 
3. Install node and its dependencies
    1. Create a file called “.bash_profile” in the home directory
    2. Close the terminal and reopen 
    3.  Run: curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
			nvm install 8.9.4
			npm i -g npm
			npm install -g cordova
			npm install -g ionic
4. Install Xcode
    1. Open the App Store, find Xcode and install 
        1. If you don’t have an Apple ID create one
        2. Choose none for credit card and include DePauw address for the billing address
    2. In the Xcode app select Xcode from menu bar. Then click Open Developer Tools —> more developer tools
    3. This will open a page called more downloads for apple developers in the browser. You will have to enter your apple credentials if you aren’t already logged in
    4. Select the newest version of Command line tools for Xcode (DO NOT CLICK THE BETA VERSION). Click the dmg file to download it
    5. In the terminal run $ sudo xcode-select -s /Applications/Xcode.app/Contents/Developer
5. Sign up for an Apple Developer account
    1. Go to https://appleid.apple.com/account
    2. Enter your information, make sure to use organization email address
6. Download Apple certificate (THIS IS CENTENE SPECIFIC)
    1. Go to "https://developer.apple.com/account/resources/certificates/list" and sign in with your Centene Apple ID
    2. Download the certificate called Centene Corporation created by Sonika Dabbi
    3. Ask another mobile developer to export the private key from Keychain, and add that to your Keychain.
7. Install Android Studio
    1. Install Android Studio from https://developer.android.com/studio/. This will install the SDK as well 
    2. Add the following to the folder .bash_profile:
        1. export ANDROID_HOME=<SDK path>
        2. export PATH=${PATH}:/${ANDROID_HOME}/platform-tools:/${ANDROID_HOME}/tools
    3. <SDK PATH> is the location where the android SDK was installed. To find it, click Android Studio fro the menu bar. Go to Preferences —> appearances and behavior —> system settings —> android sdk. You will find the path next to Android SDK Location
    4. Ensure that SDK platforms from 5.0 (Lollipop) and above are installed 
    5. Run the following in the Terminal in your home directory to install Gradle
        1. Brew install gradle 
        2. (Installing homebrew) https://brew.sh/ 
    6. Add the passwords for the keystrokes to .bash_profile (ask another dev for them (CENTENE))
8. Sign up for a google developer account
    1. Go to https://accounts.google.com/SignUp
    2. Enter in info, for username use DePauw email address
    3. Notify an admin to add you to the developer portal as an admin
9. Sign up for Ionic
    1. In the terminal run 
        1. $ ionic signup
    2. Ionic signups will open in the browser 
    3. Enter your name, depauw address an password
10. Add SSH key to bitbucket and gitlab (Centene Specific)
        1. Bitbucket
            1. Go to https://bitbucket.centene.com and log in
            2. If you have not been provisioned, please inform your manager or lead.
            3. Once logged in, click on your profile icon at the top right of the site and select Manage Account
            4. Select SSH keys in the left menu
            5. Open your terminal and enter
                1. ssh-keygen -t rsa -C "YOUREMAIL@centene.com
            6. "The terminal will say: "Enter file in which to save the key (/Users/cn222812/.ssh/id_rsa):” Hit Enter
            7. It may ask you for a password. Enter a password of your choosing, and then confirm
            8. Then enter: $ pbcopy < ~/.ssh/id_rsa.pub This will copy your key to your clipboard.
            9. Go back to bitbucket and paste your SSH key in the text area and click add key
        2. Gitlab
            1. Go to https://gitlab.centene.com/ and log in
            2. Click on your profile icon in the top right corner and click ‘settings’
            3. On the menu on the left-hand side, click SSH Keys
            4. Paste your key in the text area, ensure that it has a title and click ‘add key’
11. Try Building the App
    1. Run the following commands to test. If you have not signed into Ionic before, you will be asked for your credentials
        1. Npm install 
        2. Npm run build:os
        3. Npm run build:android

## deploying to mobile
1. Navigate to you your Ionic project and run $ ionic build in the terminal 
2. Create the iOS and Android projects by running 
    1. ionic cap add ios
    2. ionic cap add android
    3. These create android and iOS folders at the root of your project 
    4. You only have to do this the first time you deploy 
3. Every time you perform a build you have to copy the changes you made into the native projects 
    1. Ionic cap copy
4. If you make any changes in the native projects, you can push it back to the source code with 
    1. Ionic cap sync

Spinning up to browser
1. Ionic serve

Deploying to iOS
1. Ionic cap open iOS
    2. Will open your native ios project in Xcode
2. Click on the app in the project navigator on the left side 
3. Click on signing and capabilities and select Centene Corporation as your team 
    4. Ensure that your bundle identifier looks like com.centene.<project_name>
4. Deploying to a device 
    1. Connect your iPhone to your Mac 
    2. On your phone, open settings -> general -> profiles and device management 
        1. Tap Apple development: your team and select Trust
    3. In Xcode click build to install and launch the app onto your apple device
5. Deploying to a simulator
    1. When Xcode opens, go to the top left where you’ll see Generic iOS device. Clicking it will open a list of devices you can deploy to 
    2. Select your preferred device and build it

Deploying to Android
1. Ionic cap open iOS
    1. Will open native project in android studio
2. To connect to an android device 
    1. Connect device to your computer (can be either Mac or pc)
    2. In android studio click the run button, select your device, then click OK to install and launch the app on the device
3. To run on an emulator
    1. Open tools —> AVD manager
    2. A window called your virtual devices will open. Click Create virtual device
    3. Select the category phone and your desired version
    4. If you want to adjust emulator properties, select New Hardware Profile
    5. Click next
    6. Select system image. API level 28 is recommended
    7. Give your device a name and click finish
    8. Exit out of virtual devices and build your app. Then click run

Troubleshooting 
* Run ionic cap copy and try building it again
* If the app wont deploy to your iPhone
    * Ensure that you have the right bundle identifier and team 
    * Update Capacitor iOS to the most recent version
▪	yarn add @capacitor/ios@latest
	▪	If a sensor or other property isn't working the way it should
    * Check your permissions 
        * iOS: App → Info → Custom iOS Target Properties
        * Android: android/app/src/main/AndroidManifest.xml and check under the Permissions section 
* Android won't build
    * Check that your SDK has downloaded 
    * Go to File → Sync Project with Gradle Files 
    * Update Capacitor Android to the most recent version 
▪	yarn add @capacitor/android@latest
	▪	Gradle Issues
    * Close out of Android Studio
    * Go to the project folder in the Finder
    * Delete the .idea directory
    * Delete the .iml files
    * Re-open Android Studio and open your project
* General issues
    * Keep Capacitor core and CLI up to date
▪	yarn add @capacitor/cli@latest yarn add @capacitor/core@latest



# Resources

## Ionic
### Ionic and React 
* [using hooks in ionic](https://ionicframework.com/blog/using-react-hooks-in-an-ionic-react-app/)


## React

* [React Master Resource](https://github.com/enaqx/awesome-react#react-general-resources)
* [React Interview Questions](https://github.com/sudheerj/reactjs-interview-questions#what-is-react)
* [Conditional Rendering](https://reactjs.org/docs/conditional-rendering.html)
* [React/Typescript Cheatsheet](https://github.com/typescript-cheatsheets/react/blob/main/README.md#basic-cheatsheet-table-of-contents)
### hooks
* [Context](https://reactjs.org/docs/context.html)
* [useEffect](https://dev.to/iquirino/react-hook-clean-up-useeffect-24e7)
* 












