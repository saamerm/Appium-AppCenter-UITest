# App Center Appium UI Tests

Primary documentation for App Center Test is available here: https://docs.microsoft.com/en-us/appcenter/test-cloud/
Skip to my notes below for simple steps to test this

# Upload commands
No matter which test framework you are using, to run UI Tests in App Center, you **must** generate a prototype upload commandline in one of the systems using the wizard. This command line requires modifications in order to be executed, which the test framework-specific upload scripts demonstrate for basic usage. 

1. Log into https://appcenter.ms
2. If you have not already created your app, do so by selecting **Add new > Add new app**. (More info: https://docs.microsoft.com/en-us/appcenter/dashboard/creating-and-managing-apps)
3. Name your app, select the target OS of your app, and the platform your app is written in. 
4. Select the **Test** icon on the left side of the screen, it is a circle with a checkmark inside of it.
5. Click **New test run**
6. Select the devices you wish to run your tests on.
7. Configure the test framework you are using.
8. On the submit screen follow the "prerequesites" step if this is your first time creating a run in AppCenter/Test. 
9. Copy the command from **Running Tests > Upload and schedule tests**. 

#### Example (Your exact command will differ)
> appcenter test run appium --app "kegr/ReadmeDemo" --devices "kegr/top-4" --app-path pathToFile.apk  --test-series "master" --locale "en_US" --build-dir target/upload

# Framework Samples in this Repo
## Appium
These samples include the App specific steps documented here: https://docs.microsoft.com/en-us/appcenter/test-cloud/preparing-for-upload/appium

- [Appium Android Sample](Appium/Android) This sample includes an APK file and a pre-written Appium test suite prepared for running in AppCenter/Test. 

- [Appium iOS Sample](Appium/iOS) This sample includes IPA & app files and a pre-written Appium test suite prepared for running in AppCenter/Test.

## Saamer's notes

### iOS tests

1. Clone the repo and Open the terminal in the `Appium-Launch-iOS-Working` directory
2. Install appcenter in your command line
```
npm install appcenter-cli -g
npm install appcenter -g
```
3. Run this command to login
```
appcenter login
```
4. Install the maven dependency libraries needed
```
mvn -DskipTests -P prepare-for-upload package
```
5. Once that succeeds (only if it succeeds), start the appcenter UI test by running this
```
appcenter test run appium --app "Sonesta/Sonesta-2" --devices 815fdb40 --app-path Sonesta.ipa --test-series "master" --locale "en_US" --build-dir target/upload
```
Note: It takes a few minutes to run, and `815fdb40` might change depending on availability. Also, device sets do not work even though they should

### Android tests

Run the same steps as above, but use the `Appium-Launch-Android-Working` directory and start the appcenter UI test by running this
```
appcenter test run appium --app "Sonesta/Sonesta-3" --devices 8cb037b0 --app-path app-release.apk --test-series "launch-tests" --locale "en_US" --build-dir target/upload
```

### Observations

I wasn't able to make any samples online of AppCenter+Appium work anywhere. However, within the command line tool, there is a `generate` command that helps you create test iOS & Android samples `appium test generate appium --platform ios --output-path iosTest/` & `appium test generate appium --platform android --output-path androidTest/`
