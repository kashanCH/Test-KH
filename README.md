# io.chealth.plugins.contour-next-one

[AliveCor Architecture](https://www.notion.so/currenthealth/AliveCor-2-0-Initiative-Overview-d2c16585f8b64acba427b7d4e46e97f2?pvs=4)

AliveCor Plugin for iOS and Android flows, to communicate with AliveCor ECG devices and Peripheral Framework.


## Owners of the repo:

- [Capybara Team](https://www.notion.so/currenthealth/Team-Capybara-00a693c44694414486c7639d15a47674)
- If you need more information about the team, feel free to visit our [Notion page](https://www.notion.so/currenthealth/Team-Capybara-00a693c44694414486c7639d15a47674).

## Regulatory Requirements

- Not applicable

#### To obtain the Kardia JWT token to run on your local machine, follow the steps below using a Docker setup.

### Install docker from [Docker](https://docs.docker.com/engine/install/)

### Ensure that you are using following docker command for kardia sandbox environment. Run below command in Terminal. 

```bash
docker run --env KARDIA_ACCESS_KEY=9htu7p3o --env KARDIA_SECRET_KEY=91zazqim --env KARDIA_ENV=sandbox -p 8080:8080 kardiasdk/kardia-auth-server ./kardia-auth-server
```

### You can now obtain the JWT using the API below with the specified body parameters. Use cURL or Postman to call the API.

API URL: http://localhost:8080/token

```bash
{
"bundleId": "com.currenthealth.byod",
"partnerId": "8xf2Z5doYNtstscdux7xcvdlnl5mbza8",
"patientMrn": "ExamplePatient MRN",
"teamId": "qNc1HfcEvMfVt7ndVqUwcvdlnl1zkrl4"
}
```

### Once the server is set up, you can run the mentioned /token service to obtain the JWT token.

#### Kardia ECG Device 

- To test, you must have a Kardia ECG device.
- The Kardia ECG device can only be tested on a real iOS or Android device with Bluetooth enabled.
- Please ensure the device is connected before running the iOS or Android app if it does not connect automatically.

#### Build project
We can run the AliveCor plugin using the following methods:
- Exmaple using Capacitor Create App
- Using Kardia SDK Sample App
- Using Raptor - No need to generate JWT token because we have PFS API to generate token automatically. 

### The exmaple of this plugin is created with Capacitor Create App

This app was created using [`@capacitor/create-app`](https://github.com/ionic-team/create-capacitor-app),
and comes with a very minimal shell for building an app.

### Running this example

To run the provided example, you can use `npm start` command.

## Install

```bash
npm install alivecor6l
npx cap sync
```

```bash
npm start
```

### Using Sample App

#### For iOS

For iOS Download SDK from [Kardia iOS SDK 1.5.1 ](https://www.notion.so/currenthealth/Team-Capybara-00a693c44694414486c7639d15a47674?pvs=4#cb84c972508a439aa0e5699b25590125)

Open the AliveCorKitExample.xcodeproj file located in the sdk folder using Xcode to test the Kardia app. Install the app on a real iOS device to test it with the Kardia ECG device.

#### For Android

For Android Download SDK from [Kardia Android SDK 1.5.1 ](https://www.notion.so/currenthealth/Team-Capybara-00a693c44694414486c7639d15a47674?pvs=4#1c11167b48cc4f2b8aeca74c82109e13)

Open the SampleApp in Android Studio located in the main SDK folder. It will install the dependencies, and once completed, you can run it on an Android device to test with the Kardia ECG device.

### Using Raptor

The following steps must be followed:

- Check out the RaptorV2 main branch from the [Repo](https://github.com/snap40/RaptorV2)
- Add the ECG device serial number in Crashboard. Contact the Capybara team to add your device.
- Follow the RaptorV2 repository README to install on iOS or Android devices.
- In the Raptor app, you can find the ECG icon under the 'New Reading' screen to initiate the ECG scanning flow.

[Building AliveCor in raptor, a (quick) guide ](https://www.notion.so/currenthealth/Building-AliveCor-in-raptor-a-quick-guide-1b9cbf3ea6c94dfbbab702d4b5ad89ca?pvs=4)

## Test

## Running Android Test Cases

Open the project in Android Studio and find the files under io.chealth.plugins.alivecor6l/android/src/test

Just run these classes using the provided Android Studio run option.

Alternatively, go into the Android directory of the plugin using the terminal and run the below command:


```bash
npm test./gradlew clean
./gradlew build
```

## Running iOS Test Cases

#### Running test cases can be done by either of the below two ways.

Navigate to the iOS folder. io.chealth.plugins.alivecor6l/iOS/AlivecorECGPluginTests

- To run all tests, go to the top menu and select Product > Test, or simply use the shortcut Command + U. 
- To run a specific test case or test method, click the diamond icon next to the test or method name in the code editor.

## Releasing

1. Run `npm version (new version number here)` to update the `package.json` and `package-lock.json` files.
2. Run `npm publish` to release to Nexus.


## Kardia Developer Guide (v. 1.5.1)

#### For Android

[Kardia Android Developer Guide ](https://www.notion.so/currenthealth/Team-Capybara-00a693c44694414486c7639d15a47674?pvs=4#4011296fa957481a839cf7c39183bf8d)

#### For iOS:- 

[Kardia iOS Developer Guide ](https://www.notion.so/currenthealth/Team-Capybara-00a693c44694414486c7639d15a47674?pvs=4#c67749f9a3a0401d931d8fc536b6f62c)


## APIs and Plugin Methods 

The `onAction` method in the provided code serves as a bridge between the plugin and the flow orchestrator, facilitating communication from the web level down to the plugin level. When triggered, this method extracts relevant context data (such as API key, server environment, and app name) and initiates the AliveCor SDK. It handles the initialization process, manages errors, and launches the appropriate activity to start the ECG reading process. This method ensures that the necessary setup is done and that the plugin can effectively interact with the hardware to perform the required actions.

### onAction(...)

- Android Plugin [OnAction ](https://github.com/snap40/io.chealth.plugins.alivecor6l/blob/main/android/src/main/java/io/chealth/plugins/AlivecorEcgPlugin.kt)

- iOS Plugin [OnAction ](https://github.com/snap40/io.chealth.plugins.alivecor6l/blob/b1890c210f6ba67a3926e816c8edc55054ce9057/ios/AlivecorECGPlugin/AlivecorECGPlugin/Classes/CapacitorPlugin/AlivecorEcgPlugin%2BCapacitor.swift#L16)  

- Web Plugin [OnAction ](https://github.com/snap40/RaptorV2/blob/71218e7ed370da6a2df07e76f5142fa4756420bc/projects/raptor-shared/src/lib/pages/configurable-reading-flow/flow-orchestrator.service.ts#L4)   

```typescript
onAction(options: { actionName: string; ourContext: any; }, onComplete: PluginCallback) => Promise<{ type: string; data: any; }>
```

#### getPresigned URL for S3 ECG file upload

We have a predefined URL that we use to pass the ECG base64 string from the plugin. Before uploading this file to S3, we first obtain a pre-signed S3 bucket URL through an API. Once we have this pre-signed URL, we convert the base64 string into an MD5 hash and then pass it along with the pre-signed URL for the upload.

```bash
curl --location -XPOST <https://dev-patient-facing.snap40.com/alivecor/upload-url
--header "Authorization: $PATIENT_ID_TOKEN"
./gradlew build
```

Presigned File Uploading [Document ](https://www.notion.so/currenthealth/Verifying-Integrity-of-Files-Uploaded-to-S3-via-a-PFS-Presigned-URL-aabaff3c6c0a41ffb4a4441fdba4d572?pvs=4)   


#### getReading

How to call it:

| actionName | Required ourContext                                           | description                                                                                                                                                                                                                |
|------------|---------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| getReading | `{ apiKey: string, aliveCorServer: string, appName: string }` | `apiKey` is the JWT for AliveCor SDK. `aliveCorServer` is the server to connect to - `PRODUCTION` or `STAGING`. `appName` is the package ID for the application. Initialises and calls the Alivecor SDK to get a reading. |

Possible responses:

| response type | description                                        | example                                                                                                                                        |
|---------------|----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| result        | The SDK took a reading and the result is enclosed. | `{ type: "result", data: { "averageHeartRate": 123, "determination: "normal", "determinationTranslationKey: "__alivecor_ecg-instruction-summary_determination_normal","nextStepsTranslationKey: "__alivecor_ecg-instruction-summary_next_steps_normal","leadType": "SIX", "generatedAt": "2023-11-24T17:07:26.718Z" }}` |
| failed        | Failed to take a reading                           | `{ type: "failed", data: { reason: string /* details for dev team */ }}`                                                                       |

## ECG Determination

The `ECGDetermination` enum represents various types of ECG analysis results. Each enum case has been mapped to custom enum case. Mapped enums will be send back to Raptor, evntually sent to Backend.

### Enum Keys

| Mapped Key                | iOS SDK Key                 | Android SDK Key         | Translation Key                                                 | Next Steps Translation Key                                     |
|---------------------------|-----------------------------|-------------------------|-----------------------------------------------------------------|---------------------------------------------------------------|
| sinus_rhythm              | normal                      | normal                  | __alivecor_ecg-instruction-summary_determination_sinus_rhythm   | __alivecor_ecg-instruction-summary_next_steps_sinus_rhythm    |
| afib                      | atrialFibrillation          | afib                    | __alivecor_ecg-instruction-summary_determination_afib           | __alivecor_ecg-instruction-summary_next_steps_afib            |
| too_short                 | tooShort                    | too_short               | __alivecor_ecg-instruction-summary_determination_too_short      | __alivecor_ecg-instruction-summary_next_steps_too_short       |
| too_long                  | tooLong                     | too_long                | __alivecor_ecg-instruction-summary_determination_too_long       | __alivecor_ecg-instruction-summary_next_steps_too_long        |
| unclassified              | unclassified                | unclassified            | __alivecor_ecg-instruction-summary_determination_unclassified   | __alivecor_ecg-instruction-summary_next_steps_unclassified    |
| bradycardia               | bradycardia                 | bradycardia             | __alivecor_ecg-instruction-summary_determination_bradycardia    | __alivecor_ecg-instruction-summary_next_steps_bradycardia     |
| tachycardia               | tachycardia                 | tachycardia             | __alivecor_ecg-instruction-summary_determination_tachycardia    | __alivecor_ecg-instruction-summary_next_steps_tachycardia     |
| no_analysis               | noAnalysis                  | no_analysis             | __alivecor_ecg-instruction-summary_determination_no_analysis    | __alivecor_ecg-instruction-summary_next_steps_no_analysis     |
| sinus_rhythm              | sinusRhythm                 | sinus_rhythm            | __alivecor_ecg-instruction-summary_determination_sinus_rhythm   | __alivecor_ecg-instruction-summary_next_steps_sinus_rhythm    |
| unreadable                | unreadable                  | unreadable              | __alivecor_ecg-instruction-summary_determination_unreadable     | __alivecor_ecg-instruction-summary_next_steps_unreadable      |
| unclassified              | unsupported                 | - *                     | __alivecor_ecg-instruction-summary_determination_unclassified   | __alivecor_ecg-instruction-summary_next_steps_unclassified    |
| sinus_rhythm,wide_qrs     | wideQRS                     | sinus_rhythm_wide_qrs   | __alivecor_ecg-instruction-summary_determination_sinus_rhythm_wide_qrs     | __alivecor_ecg-instruction-summary_next_steps_sinus_rhythm_wide_qrs     |
| sinus_rhythm,multiple_pacs| multiplePACs                | sinus_rhythm_pacs       | __alivecor_ecg-instruction-summary_determination_sinus_rhythm_multiple_pacs| __alivecor_ecg-instruction-summary_next_steps_sinus_rhythm_multiple_pacs|
| sinus_rhythm,multiple_pvcs| multipleVEBs                | sinus_rhythm_pvcs       | __alivecor_ecg-instruction-summary_determination_sinus_rhythm_multiple_pvcs| __alivecor_ecg-instruction-summary_next_steps_sinus_rhythm_multiple_pvcs|

`*` indicates that the corresponding key is not available in the SDK.

### Interfaces


#### PluginResultData


#### PluginResultError

| Prop          | Type                |
| ------------- | ------------------- |
| **`message`** | <code>string</code> |


### Type Aliases


#### PluginCallback

<code>(data: <a href="#pluginresultdata">PluginResultData</a>, error?: <a href="#pluginresulterror">PluginResultError</a>): void</code>

</docgen-api>
