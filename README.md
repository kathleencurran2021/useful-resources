# useful-resources
This repo has code snippets, directions, resources, etc, to use as a reference


[Mobile](#mobile)
* [Setting Up the Environment](#mobile-dev-environment-setup)
* [Deploying](#deploying)
* [Troubleshooting](#troubleshooting)

[Ionic](#ionic)
* [Gestures](#gestures)
* [Persisting](#persisting-data)
* [Platform Specific](#platform-specific)
* [Authentication](#authentication)
* [Capacitor](#capacitor)
* [Ionic React](#ionic-and-react)


[React](#react)
* [Components](#components)
* [Routing](#routing)
* [Interface](#interface)
* [Hooks](#hooks)
* [Styled Components](#styled-components)


[Other](#other)
* [Git Resources](#git-resources)
* [Terminal](#terminal)
* [npm](#npm-packaging)
* [Lerna](#lerna)
* [JavaScript](#javascript)
* [Testing](#testing)




# Mobile 
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

## Deploying
						       
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

### Spinning up to browser
1. Ionic serve

### Deploying to iOS
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

### Deploying to Android
1. Ionic cap open android
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
	
## Troubleshooting

### Deployment Troubleshooting 
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

	
### Mobile Troubleshooting
* [Cannot find module error](https://stackoverflow.com/questions/54695891/cannot-find-module-for-my-own-typescript-module)
* [Gradle issue](https://stackoverflow.com/questions/30142056/error-unfortunately-you-cant-have-non-gradle-java-modules-and-android-gradle)

**Tips**
* IF you’re getting that massive babel-loader error and the app won’t spin up on screen --> Delete node_modules from the portal files 
* If you get the route outside of router error --> Uninstall react-router-dom and reinstall
* IF vscode can’t find any of your modules --> Run yarn in the affected package




# Ionic
* [Ionic 6](https://ionicframework.com/docs/intro/upgrading-to-ionic-6)
* [Ionic Tutorials](https://ionicthemes.com/tutorials/tag/capacitor)

## Gestures
* [Gestures](https://ionicframework.com/docs/utilities/gestures)
* [Tinder Swipe Cards w Gestures](https://www.joshmorony.com/create-tinder-style-swipe-cards-with-ionic-gestures/)
* [Custom Gestures](https://ionicacademy.com/custom-gestures-ionic/)
* [Add UX through double taps](https://medium.com/@JordanBenge/ionic-4-quickly-add-ux-through-the-use-of-double-taps-5f6e3216a289)


## Persisting Data
* [Persisting React State](https://dev.to/selbekk/persisting-your-react-state-in-9-lines-of-code-9go)
* [Persistent Global Store](https://dev.to/bigaru/creating-persistent-synchronized-global-store-using-react-hooks-in-typescript-209a)
* [Global Cached State](https://medium.com/@akrush95/global-cached-state-in-react-using-hooks-context-and-local-storage-166eacf8ab46)
* [LocalStorage()](https://usehooks-ts.com/react-hook/use-local-storage)
	
	
## Platform Specific

### iOS
* [Configuring iOS](https://capacitorjs.com/docs/ios/configuration)
* [Safe Area Inset](https://www.quirksmode.org/blog/archives/2017/10/safeareainset_v.html)
* [Designing Websites for iphone 10](https://webkit.org/blog/7929/designing-websites-for-iphone-x/)
* [Redirect URI - Stackoverflow](https://stackoverflow.com/questions/53692030/custom-redirect-uri-to-macos-app-not-working)
* [Provisioning Profile](https://clearbridgemobile.com/how-to-create-a-distribution-provisioning-profile-for-ios/)
* [URL Scheme Handling](https://stackoverflow.com/questions/16226240/handling-different-url-schemes-in-ios-facebook-and-instagram)
* [Cocoapods](https://guides.cocoapods.org/using/getting-started.html)

### Android
* [Configuring Android](https://capacitorjs.com/docs/android/configuration)


## Authentication 
* [Identity Vault](https://ionic.io/docs/identity-vault)
* [Google Login Capacitor](https://enappd.com/blog/google-login-in-ionic-react-capacitor-apps/122/)
* [Auth0 Ionic](https://auth0.com/docs/quickstart/native/ionic4/01-login?_ga=2.243705925.1180762906.1594330750-437815093.1594330749)
* [Managing Authentication with Context](https://dev.to/aaronksaunders/learn-to-build-mobile-apps-with-ionic-framework-reactjs-and-capacitor-manage-authentication-state-using-react-context-api-n9j)
* [Maintain User state on refresh](https://stackoverflow.com/questions/58879856/how-to-maintain-the-authenticated-user-state-on-page-refresh-with-react)
* [Okta build an Ionic app with User Auth](https://developer.okta.com/blog/2017/08/22/build-an-ionic-app-with-user-authentication)
* [Pingone setup iOS](https://github.com/pingidentity/pingone-sample-native-mobile#ios-setup)
* [AppAuth](https://github.com/openid/AppAuth-JS/issues/8)
* [Pingone API reference](https://apidocs.pingidentity.com/pingone/platform/v1/api/)
* [Authenticate React with Auth0](https://auth0.com/authenticate/react/ping-federate/)
* [JWTs in react secure authentication](https://developer.okta.com/blog/2019/10/02/jwt-react-auth)
	
## Ionic and React 
* [using hooks in ionic](https://ionicframework.com/blog/using-react-hooks-in-an-ionic-react-app/)
* [React Navigation in Ionic](https://ionicframework.com/docs/react/navigation)
* [More React Navigation](https://www.digitalocean.com/community/tutorials/ionic-ionic-4-react-navigation)
* [Ionic React Quickstart](https://ionicframework.com/docs/react/quickstart)
	
	
## Capacitor
	
* [Capacitor - Mobile and PWA](https://ionicframework.com/resources/webinars/capacitor-2-launch?utm_campaign=capacitor&utm_source=hs_email&utm_medium=email&utm_content=88296761&_hsenc=p2ANqtz-_FHTIb4SiWJzC1f-LuItxTGDat_uZNLik1AS8bBwoPGSE7OZwW2wHoX27uX_bWth0YhtNYs3DjW6wP__h7eaKl3viwgg&_hsmi=88296761)
* [Building a Capacitor App](https://capacitorjs.com/docs/basics/building-your-app)
* [isPlatform method](https://ionicframework.com/docs/react/platform)
* [inAppBrowser](https://ionicframework.com/docs/native/in-app-browser/)
* [adding multiple components to ionic app](https://levelup.gitconnected.com/adding-multiple-components-to-your-ionic-application-8ba5d5523aa7)
* [Common Config](https://capacitorjs.com/docs/basics/configuring-your-app#common-configuration)
* [Deep Linking](https://capacitorjs.com/docs/guides/deep-links)
* [Background Mode Docs](https://ionicframework.com/docs/native/background-mode/)
* [ionic-storage](https://github.com/ionic-team/ionic-storage/blob/main/examples/react/src/App.tsx)
* [Data Storage](https://ionicframework.com/docs/react/storage)

### Local Notifications
* [Firebast Push Notifications using Capacitor](https://enappd.com/blog/firebase-push-notification-in-ionic-react-capacitor/111/)
* [Ionic React Local Notifications using Capacitor](https://blog.chinaza.dev/ionic-react-local-notifications-using-capacitor)
* [Local Notifications Example](https://github.com/ionic-team/capacitor-testapp/blob/main/src/components/LocalNotificationTest.tsx)
* [Creating Capacitor Local Notifications with sound and actions buttons](https://www.youtube.com/watch?v=bww4a4B43tM)
* [Local Notifications Docs](https://ionicframework.com/docs/v3/native/local-notifications/)
	

# React

* [React Master Resource](https://github.com/enaqx/awesome-react#react-general-resources)
* [React Interview Questions](https://github.com/sudheerj/reactjs-interview-questions#what-is-react)
* [Conditional Rendering](https://reactjs.org/docs/conditional-rendering.html)
* [React/Typescript Cheatsheet](https://github.com/typescript-cheatsheets/react/blob/main/README.md#basic-cheatsheet-table-of-contents)
* [React Bootstrap](https://react-bootstrap.github.io/getting-started/introduction/)
* [Setting up React, Webpack, and Babel](https://www.valentinog.com/blog/webpack/#how-to-set-up-react-webpack-5-and-babel-from-scratch)
* [React Props Cheatsheet](https://www.freecodecamp.org/news/react-props-cheatsheet/)

## Components
* [Extending Components](https://www.pluralsight.com/guides/use-interface-props-in-functional-components-using-typescript-with-react)
* [Opening and Closing Modals in Different Components](https://stackoverflow.com/questions/61864072/trying-to-open-and-close-a-modal-in-different-components)

## Routing
* [React Router](https://reactrouter.com/web/api/Switch)
* [React Router Example](https://github.com/thanhbinhtran93/react-router-example/tree/master/src)

	
## Interface
* [Interface Props in Functional Components](https://www.pluralsight.com/guides/use-interface-props-in-functional-components-using-typescript-with-react)
* [Interfaces in Typescript](https://blog.logrocket.com/interfaces-in-typescript-what-are-they-and-how-do-we-use-them-befbc69b38b3/)
* [Change Button color on Click](https://stackoverflow.com/questions/60929233/how-to-change-buttons-color-on-click-of-button-in-ionic-4)
* [Set a style of a focused element dynamically](https://forum.ionicframework.com/t/set-style-of-a-focused-element-dynamically/135642)
	
## Hooks
* [Context](https://reactjs.org/docs/context.html)
* [useEffect](https://dev.to/iquirino/react-hook-clean-up-useeffect-24e7)

## Styled Components
* [Styled Component Basics](https://styled-components.com/docs/basics)
* [Styled Components React Native](https://levelup.gitconnected.com/using-styled-components-with-react-native-de645fcf4787)
* [Sass](https://sass-lang.com/)

### Practice Examples 
* [Movie Star UI](https://github.com/aagavin/movie-star-ui/tree/master/src)
* [React Masterminds](https://github.com/drminnaar/react-masterminds)

	

# Other
	
## Git Resources
* [Adding SSH key to agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)
* [Adding SSH to Github](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)
* [Merge Conflicts](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-using-the-command-line)
	
## Terminal 
* [Master List of Linux Commands](https://kinsta.com/blog/linux-commands/)
	
### Troubleshooting
* [Git Troubleshooting](https://dangitgit.com/en)
* [Error couldn't read from remote repository](https://stackoverflow.com/questions/30068298/git-fatal-could-not-read-from-remote-repository-please-make-sure-you-have-th)
	

## npm Packaging
* [import component outside src directory](https://stackoverflow.com/questions/49705170/reactjs-import-component-outside-src-directory)
* [Create a React npm package](https://www.codementor.io/@peterodekwo/create-a-simple-react-npm-package-in-simple-steps-using-cra-w966okagi)
* [Guide to publishing a react package to npm](https://blog.logrocket.com/the-complete-guide-to-publishing-a-react-package-to-npm/)
* [Package React Component to distribute](https://itnext.io/how-to-package-your-react-component-for-distribution-via-npm-d32d4bf71b4f)
* [multiple output paths in Webpack](https://stackoverflow.com/questions/35903246/how-to-create-multiple-output-paths-in-webpack-config)

## Lerna
* [Lerna, TS, CRA, and Storybook](https://dev.to/shnydercom/monorepos-lerna-typescript-cra-and-storybook-combined-4hli)
* [Monorepo Setup](https://medium.com/@sisosys7/a-monorepo-setup-with-lerna-react-and-typescript-7b912fb48622)
* [Short Lerna tutorial](https://medium.com/shopback-engineering/lerna-tutorial-series-brief-f77f40c5777f)

## JavaScript
* [Promises vs Async Await](https://medium.com/better-programming/should-i-use-promises-or-async-await-126ab5c98789#:~:text=Promise%20creation%20starts%20the%20execution,have%20any%20effect%20on%20it.)
* [Optional Chaining](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Optional_chaining)

## Testing
* [Jest test React apps](https://jestjs.io/docs/en/tutorial-react)
* [jest mocks](https://medium.com/@rickhanlonii/understanding-jest-mocks-f0046c68e53c)
* [Cypress Beginner Tutorial](https://www.valentinog.com/blog/cypress/)
* [Cypress Login SSO Recipe](https://github.com/cypress-io/cypress-example-recipes/blob/master/examples/logging-in__single-sign-on/cypress/integration/logging-in-single-sign-on-spec.js)

Running a Jest Test
1. Know the name of the test you’re trying to run 
2. Pull up the terminal
3. Navigate to the portal folder
4. Run $ yarn test
    1. This will run all the tests in the repository. Press any key to quit
5. Press ‘P’ and search for the test you want to run 


	

# Other Useful Resources
[Nicole Google Drive](https://drive.google.com/drive/folders/1J3aDFuuHbQnJTtD5t2IWK7Q57JoiTalo?usp=sharing)

[Rudy Resource](https://github.com/rwschmitz/useful-information)

