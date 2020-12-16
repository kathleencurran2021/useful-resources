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

