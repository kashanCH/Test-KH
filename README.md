# io.chealth.plugins.contour-next-one

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
- Using Raptor

### The exmaple of this plugin is created with Capacitor Create App

This app was created using [`@capacitor/create-app`](https://github.com/ionic-team/create-capacitor-app),
and comes with a very minimal shell for building an app.

### Running this example

To run the provided example, you can use `npm start` command.

```bash
npm start
```

### Using Sample App

#### For iOS

For iOS Download SDK from [Kardia iOS SDK 1.5.1 ](https://www.notion.so/currenthealth/Team-Capybara-00a693c44694414486c7639d15a47674?pvs=4#cb84c972508a439aa0e5699b25590125)

Open the AliveCorKitExample.xcodeproj file located in the sdk folder using Xcode to test the Kardia app. Install the app on a real iOS device to test it with the Kardia ECG device.

#### For iOS

For Android Download SDK from [Kardia Android SDK 1.5.1 ](https://www.notion.so/currenthealth/Team-Capybara-00a693c44694414486c7639d15a47674?pvs=4#1c11167b48cc4f2b8aeca74c82109e13)

Open the SampleApp in Android Studio located in the main SDK folder. It will install the dependencies, and once completed, you can run it on an Android device to test with the Kardia ECG device.

#### Using Raptor

Following steps must be followed

- Checkout RaptorV2 Main Branch from [Repo](https://github.com/snap40/RaptorV2)
- Add ECG device serial number in crashbaord. Contact with Capybara team to add yoru device.
- Follwoing RapotorV2 Read to install on iOS or Android Devices.
- In Raptor App you can find ECG ICON under New Reading Screen to initiate the ECG scanning flow. 






## Install

```bash
npm install alivecor6l
npx cap sync
```

## Releasing

1. Run `npm version (new version number here)` to update the `package.json` and `package-lock.json` files.
2. Run `npm publish` to release to Nexus.


## API

<docgen-index>

* [`onAction(...)`](#onaction)
* [Interfaces](#interfaces)
* [Type Aliases](#type-aliases)

</docgen-index>

<docgen-api>
<!--Update the source file JSDoc comments and rerun docgen to update the docs below-->

### onAction(...)

```typescript
onAction(options: { actionName: string; ourContext: any; }, onComplete: PluginCallback) => Promise<{ type: string; data: any; }>
```

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
