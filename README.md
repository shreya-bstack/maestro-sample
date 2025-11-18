# maestro-sample
This repo contains a sample test suite that can be used to run maestro tests on App Automate. 

### To Run tests:
App for android: `sample_apps/sample_android.apk`  
App for iOS: `sample_apps/sample_ios.ipa`  
Upload the app using the command:
```
curl -u "<username>:<accesskey>" \
-X POST "https://api-cloud.browserstack.com/app-automate/upload" \
-F "file=@<path_to_app>"
```  
This should generate and return an app hash.

__Test Suite__: `tests/`  
zip the `tests/` folder before uploading, and upload using the command:
```
curl -u "<username>:<accesskey>" \
-X POST "https://api-cloud.browserstack.com/app-automate/maestro/v2/test-suite" \
-F "file=@<path_to_zipped_testsuite>" \
-F "custom_id=maestro_sample_tests"
```  
This should generate and return a test suite hash.

Once the app and the zipped test suite are uploaded, use the following command to run tests:  
For Android:
```
curl -u "<username>:<accesskey>" \
  -X POST "https://api-cloud.browserstack.com/app-automate/maestro/v2/android/build" \
  -H "Content-Type: application/json" \
  -d '{
    "app": "bs://<app-hash>",
    "testSuite": "bs://<test-suite-hash>",
    "project": "Maestro_Sample_Repo", 
    "execute": ["android-flow.yaml"],
    "devices": [
      "Google Pixel 9-16.0",
      "Samsung Galaxy S22-14.0",
      "Samsung Galaxy Tab S11-16.0"
    ]
  }'
``` 

For iOS:
```
curl -u "<username>:<accesskey>" \
  -X POST "https://api-cloud.browserstack.com/app-automate/maestro/v2/ios/build" \
  -H "Content-Type: application/json" \
  -d '{
    "app": "bs://<app-hash>",
    "testSuite": "bs://<test-suite-hash>",
    "project": "<Maestro Demo>", 
    "execute": ["ios-flow.yaml"],
    "devices": [
      "iPhone 15-17.0",
      "iPhone 12 Pro Max-16.0",
      "iPad Pro 11 2021-18.0"
    ]
  }'
``` 
This parallelly runs tests on the devices listed in the above command. 