# maestro-sample
This repo contains a sample test suite that can be used to run maestro tests on App Automate. 

### Run tests for android:
App: `sample_apps/sample.apk`  
Test Suite: `tests/`  
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