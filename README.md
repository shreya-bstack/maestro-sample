# maestro-sample
This repo contains a sample test suite that can be used to run maestro tests on App Automate. 

### To Run tests:
App for android: `sample_apps/sample_android.apk`  
App for iOS: `sample_apps/sample_ios.ipa`
Upload the app using the command:
```
curl -u "<username>:<accesskey>" \
-X POST "https://api-cloud.browserstack.com/app-automate/upload" \
-F "file=@.<path_to_app>"
```  
This should generate and return an app id.

__Test Suite__: `tests/`  
zip the `tests/` folder before uploading, and upload using the command:
```
curl -u "<username>:<accesskey>" \
-X POST "https://api-cloud.browserstack.com/app-automate/maestro/v2/test-suite" \
-F "file=@<path_to_zipped_testsuite>" \
-F "custom_id=maestro_sample_tests"
```  
This should generate and return a test suite id.

Once the app and the zipped test suite are uploaded, use the following command to run tests:
```
curl -u "<username>:<accesskey>" \
  -X POST "https://api-cloud.browserstack.com/app-automate/maestro/v2/android/build" \
  -H "Content-Type: application/json" \
  -d '{
    "app": "bs://<app-id>",
    "testSuite": "bs://<test-suite-id>",
    "project": "Maestro_Sample_Repo", 
    "tags": {"includeTags": ["android"]},
    "devices": [
      "Google Pixel 9-16.0"
    ]
  }'
```  