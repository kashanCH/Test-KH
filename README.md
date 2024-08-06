# io.chealth.plugins.contour-next-one

AliveCor Plugin for iOS and Android flows, to communicate with AliveCor ECG devices and Peripheral Framework.


## Owners of the repo:

- [Capybara Team](https://www.notion.so/currenthealth/Team-Capybara-00a693c44694414486c7639d15a47674)
- If you need more information about the team, feel free to visit our [Notion page](https://www.notion.so/currenthealth/Team-Capybara-00a693c44694414486c7639d15a47674).

## Regulatory Requirements

- Not applicable

## Local Development:
With regards to the local development and testing the plugins you can refer to the [Test Example ](https://github.com/snap40/io.chealth.plugins.alivecor6l/tree/main/example)

## Installing Plugin into the project

```bash
npm install @currenthealth/io.chealth.plugins.alivecor.ecg
npm cap sync
```

```bash
npx cap sync
```

#### Prerequisites
Developer should have Android Studio and XCode installed in their system for Android and iOS Builds respectively.

## Build
### Download all the dependencies and build the js project
`npm install`

### For Android
#### Open Android studio
`npx cap open android`

#### API to get token on local machine
http://localhost:8080/token

```bash
{
"bundleId": "com.currenthealth.byod",
"partnerId": "8xf2Z5doYNtstscdux7xcvdlnl5mbza8",
"patientMrn": "ExamplePatient MRN",
"teamId": "qNc1HfcEvMfVt7ndVqUwcvdlnl1zkrl4"
}
```
### Note: you can generate the authentication token using docker. Install docker from [Docker](https://docs.docker.com/engine/install/)

### ensure that you the following docker command for kardia sandbox environment 

```bash
docker run --env KARDIA_ACCESS_KEY=9htu7p3o --env KARDIA_SECRET_KEY=91zazqim --env KARDIA_ENV=sandbox -p 8080:8080 kardiasdk/kardia-auth-server ./kardia-auth-server
```
### Once server setup you can run the above mentioend /token service to get the JWT token. 

## The exmaple of this plugin is created with Capacitor Create App

This app was created using [`@capacitor/create-app`](https://github.com/ionic-team/create-capacitor-app),
and comes with a very minimal shell for building an app.

### Running this example

To run the provided example, you can use `npm start` command.

```bash
npm start
```

#### Kardia ECG Device 

- To test you must have Kardia ECG device.
- Kardia ECG device test only possible on real iOS and Android device with blutooth enabled.
- Please make sure you connect the device before running the iOS or Android if its not connected automatcially. 

#### Build project
There are two ways to run the alivecor plugin
- Using Sample App
- Using Raptor

#### Using Sample App

For iOS Download SDK from [Kardia iOS SDK 1.5.1 ](https://www.notion.so/currenthealth/Team-Capybara-00a693c44694414486c7639d15a47674?pvs=4#cb84c972508a439aa0e5699b25590125)

Open the AliveCorKitExample.xcodeproj file located in the sdk folder using Xcode to test the Kardia app. Install the app on a real iOS device to test it with the Kardia ECG device.

For Android Download SDK from [Kardia Android SDK 1.5.1 ](https://www.notion.so/currenthealth/Team-Capybara-00a693c44694414486c7639d15a47674?pvs=4#1c11167b48cc4f2b8aeca74c82109e13)

Open the SampleApp in Android Studio located in the main SDK folder. It will install the dependencies, and once completed, you can run it on an Android device to test with the Kardia ECG device.


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
