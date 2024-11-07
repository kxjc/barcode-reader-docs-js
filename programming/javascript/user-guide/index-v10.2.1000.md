---
layout: default-layout
title: v10.2.10 User Guide - Dynamsoft Barcode Reader JavaScript Edition
description: This is the user guide of Dynamsoft Barcode Reader JavaScript SDK.
keywords: user guide, javascript, js
breadcrumbText: User Guide
noTitleIndex: true
needGenerateH3Content: true
needAutoGenerateSidebar: true
schema: schemas/dynamsoft-facilitates-mit-research-schema.json
---

<!--The original doc is hosted here => https://github.com/dynamsoft-docs/barcode-reader-docs-js/blob/main/programming/javascript/user-guide/index.md -->

# Barcode Reader for Your Website - User Guide

[Dynamsoft Barcode Reader JavaScript Edition](https://www.dynamsoft.com/barcode-reader/sdk-javascript/) (DBR-JS) is equipped with industry-leading algorithms for exceptional speed, accuracy and read rates in barcode reading. Using its well-designed API, you can turn your web page into a barcode scanner with just a few lines of code.

![version](https://img.shields.io/npm/v/dynamsoft-barcode-reader.svg)
![downloads](https://img.shields.io/npm/dm/dynamsoft-barcode-reader.svg)
![jsdelivr](https://img.shields.io/jsdelivr/npm/hm/dynamsoft-barcode-reader.svg)

![version](https://img.shields.io/npm/v/dynamsoft-javascript-barcode.svg)
![downloads](https://img.shields.io/npm/dm/dynamsoft-javascript-barcode.svg)
![jsdelivr](https://img.shields.io/jsdelivr/npm/hm/dynamsoft-javascript-barcode.svg)

Once the DBR-JS SDK gets integrated into your web page, your users can access a camera via the browser and read barcodes directly from its video input.

In this guide, you will learn step by step on how to integrate the DBR-JS SDK into your website.

<span style="font-size:20px">Table of Contents</span>

- [Barcode Reader for Your Website - User Guide](#barcode-reader-for-your-website---user-guide)
  - [Hello World - Simplest Implementation](#hello-world---simplest-implementation)
    - [Understand the code](#understand-the-code)
      - [About the code](#about-the-code)
    - [Run the example](#run-the-example)
  - [Building your own page](#building-your-own-page)
    - [Include the SDK](#include-the-sdk)
      - [Use a public CDN](#use-a-public-cdn)
      - [Host the SDK yourself (optional)](#host-the-sdk-yourself-optional)
    - [Prepare the SDK](#prepare-the-sdk)
      - [Specify the license](#specify-the-license)
      - [Specify the location of the "engine" files (optional)](#specify-the-location-of-the-engine-files-optional)
    - [Set up and start image processing](#set-up-and-start-image-processing)
      - [Preload the module](#preload-the-module)
      - [Create a CaptureVisionRouter object](#create-a-capturevisionrouter-object)
      - [Connect an image source](#connect-an-image-source)
      - [Register a result receiver](#register-a-result-receiver)
      - [Start the process](#start-the-process)
    - [Customize the process](#customize-the-process)
      - [Adjust the preset template settings](#adjust-the-preset-template-settings)
        - [Change barcode settings](#change-barcode-settings)
        - [Retrieve the original image](#retrieve-the-original-image)
        - [Change reading frequency to save power](#change-reading-frequency-to-save-power)
        - [Specify a scan region](#specify-a-scan-region)
      - [Edit the preset templates directly](#edit-the-preset-templates-directly)
      - [Filter the results (Important)](#filter-the-results-important)
        - [Option 1: Verify results across multiple frames](#option-1-verify-results-across-multiple-frames)
        - [Option 2: Eliminate redundant results detected within a short time frame](#option-2-eliminate-redundant-results-detected-within-a-short-time-frame)
      - [Add feedback](#add-feedback)
    - [Customize the UI](#customize-the-ui)
  - [API Documentation](#api-documentation)
  - [System Requirements](#system-requirements)
  - [How to Upgrade](#how-to-upgrade)
  - [Release Notes](#release-notes)
  - [Next Steps](#next-steps)

**Popular Examples**

- Hello World - [Github](https://github.com/Dynamsoft/barcode-reader-javascript-samples/blob/v10.2.10/hello-world/hello-world.html) \| [Run](https://demo.dynamsoft.com/Samples/DBR/JS/hello-world/hello-world.html?ver=10.2.10&utm_source=guide)
- Angular App - [Github](https://github.com/Dynamsoft/barcode-reader-javascript-samples/blob/v10.2.10/hello-world/angular) \| [Run](https://demo.dynamsoft.com/Samples/DBR/JS/hello-world/angular/dist/dbrjs-sample-angular/browser/?ver=10.2.10&utm_source=guide)
- React App - [Github](https://github.com/Dynamsoft/barcode-reader-javascript-samples/blob/v10.2.10/hello-world/react) \| [Run](https://demo.dynamsoft.com/Samples/DBR/JS/hello-world/react/build/?ver=10.2.10&utm_source=guide)
- Vue App - [Github](https://github.com/Dynamsoft/barcode-reader-javascript-samples/blob/v10.2.10/hello-world/vue) \| [Run](https://demo.dynamsoft.com/Samples/DBR/JS/hello-world/vue/dist/?ver=10.2.10&utm_source=guide)
- PWA App - [Github](https://github.com/Dynamsoft/barcode-reader-javascript-samples/blob/v10.2.10/hello-world/pwa) \| [Run](https://demo.dynamsoft.com/Samples/DBR/JS/hello-world/pwa/helloworld-pwa.html?ver=10.2.10&utm_source=guide)
- WebView in Android and iOS - [Github](https://github.com/Dynamsoft/barcode-reader-javascript-samples/tree/v10.2.10/hello-world/webview)
- Read Driver Licenses - [Github](https://github.com/Dynamsoft/barcode-reader-javascript-samples/blob/v10.2.10/use-case/read-a-drivers-license/index.html) \| [Run](https://demo.dynamsoft.com/samples/dbr/js/use-case/read-a-drivers-license/index.html?ver=10.2.10&utm_source=guide)
- Fill A Form - [Github](https://github.com/Dynamsoft/barcode-reader-javascript-samples/blob/v10.2.10/use-case/fill-a-form-with-barcode-reading.html) \| [Run](https://demo.dynamsoft.com/samples/dbr/js/use-case/fill-a-form-with-barcode-reading.html?ver=10.2.10&utm_source=guide)
- Show result information on the video - [Github](https://github.com/Dynamsoft/barcode-reader-javascript-samples/blob/v10.2.10/use-case/show-result-texts-on-the-video.html) \| [Run](https://demo.dynamsoft.com/Samples/DBR/JS/use-case/show-result-texts-on-the-video.html?ver=10.2.10&utm_source=guide)
- Debug Camera and Collect Video Frame - [Github](https://github.com/Dynamsoft/barcode-reader-javascript-samples/blob/v10.2.10/others/debug)

You can also:

- Try the Official Demo - [Run](https://demo.dynamsoft.com/barcode-reader-js/?ver=10.2.10&utm_source=guide) \| [Github](https://github.com/Dynamsoft/barcode-reader-javascript-demo/)
- Try Online Examples - [Run](https://demo.dynamsoft.com/Samples/DBR/JS/index.html?ver=10.2.10&utm_source=guide) \| [Github](https://github.com/Dynamsoft/barcode-reader-javascript-samples/tree/v10.2.10/)

## Hello World - Simplest Implementation

Let's start with the "Hello World" example of the DBR-JS SDK which demonstrates how to use the minimum code to enable a web page to read barcodes from a live video stream.  

**Basic Requirements**
  - Internet connection
  - [A supported browser](#system-requirements)
  - Camera access

### Understand the code

The complete code of the "Hello World" example is shown below

```html
<!DOCTYPE html>
<html>
<body>
<div id="camera-view-container" style="width: 100%; height: 60vh"></div>
<textarea id="results" style="width: 100%; min-height: 10vh; font-size: 3vmin; overflow: auto" disabled></textarea>
<script src="https://cdn.jsdelivr.net/npm/dynamsoft-barcode-reader-bundle@10.2.1000/dist/dbr.bundle.js"></script>
<script>
  Dynamsoft.License.LicenseManager.initLicense("DLS2eyJvcmdhbml6YXRpb25JRCI6IjIwMDAwMSJ9");
  Dynamsoft.Core.CoreModule.loadWasm(["dbr"]);
  (async () => {
    let cvRouter = await Dynamsoft.CVR.CaptureVisionRouter.createInstance();

    let cameraView = await Dynamsoft.DCE.CameraView.createInstance();
    let cameraEnhancer = await Dynamsoft.DCE.CameraEnhancer.createInstance(cameraView);
    document.querySelector("#camera-view-container").append(cameraView.getUIElement());
    cvRouter.setInput(cameraEnhancer);

    const resultsContainer = document.querySelector("#results");
    cvRouter.addResultReceiver({ onDecodedBarcodesReceived: (result) => {
      if (result.barcodeResultItems.length > 0) {
        resultsContainer.textContent = '';
        for (let item of result.barcodeResultItems) {
          resultsContainer.textContent += `${item.formatString}: ${item.text}\n\n`;
        }
      }
    }});

    let filter = new Dynamsoft.Utility.MultiFrameResultCrossFilter();
    filter.enableResultCrossVerification("barcode", true);
    filter.enableResultDeduplication("barcode", true);
    await cvRouter.addResultFilter(filter);

    await cameraEnhancer.open();
    await cvRouter.startCapturing("ReadSingleBarcode");
  })();
</script>
</body>
</html>
```

<!--TOM: Update the code links-->

<p align="center" style="text-align:center; white-space: normal; ">
  <a target="_blank" href="https://github.com/Dynamsoft/barcode-reader-javascript-samples/blob/v10.2.10/hello-world/hello-world.html" title="Code in Github" style="text-decoration:none;">
    <img src="https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/github.svg" alt="Code in Github" width="20" height="20" style="width:20px;height:20px;">
  </a>
  &nbsp;
  <a target="_blank" href="https://jsfiddle.net/DynamsoftTeam/csm2f9wb/" title="Run via JSFiddle" style="text-decoration:none;">
    <img src="https://cdn.jsdelivr.net/npm/simple-icons@3.0.1/icons/jsfiddle.svg" alt="Run via JSFiddle" width="20" height="20" style="width:20px;height:20px;" >
  </a>
  &nbsp;
  <a target="_blank" href="https://demo.dynamsoft.com/Samples/DBR/JS/hello-world/hello-world.html?ver=10.2.10&utm_source=guide" title="Run in Dynamsoft" style="text-decoration:none;">
    <img src="https://cdn.jsdelivr.net/npm/@fortawesome/fontawesome-free@6.0.0/svgs/solid/circle-play.svg" alt="Run in Dynamsoft" width="20" height="20" style="width:20px;height:20px;">
  </a>
</p>

> Don't want to deal with too many details? We also have an **out-of-the-box** version:
> 
> [Easy Barcode Scanner >>](https://github.com/Dynamsoft/easy-barcode-scanner) available for your reference.
> ```js
> // Scan instantly with a single function!
> alert(await EasyBarcodeScanner.scan());
>

-----

#### About the code

- `Dynamsoft.License.LicenseManager.initLicense()`: This method initializes the license for using the SDK in the application. Note that the string "**DLS2eyJvcmdhbml6YXRpb25JRCI6IjIwMDAwMSJ9**" used in this example points to an online license that requires a network connection to work. Read more on [Specify the license](#specify-the-license).

- `Dynamsoft.Core.CoreModule.loadWasm(["dbr"])`: This is an optional code. Used to load wasm resources in advance, reducing latency between video playing and barcode decoding.

- `Dynamsoft.CVR.CaptureVisionRouter.createInstance()`: This method creates a `CaptureVisionRouter` object `cvRouter` which controls the entire process in three steps:
  - **Retrieve Images from the Image Source**
    - `cvRouter` connects to the image source through the [ImageSourceAdapter](https://www.dynamsoft.com/capture-vision/docs/core/architecture/input.html#image-source-adapter?lang=js) interface with the method `setInput()`.
      ```js
      cvRouter.setInput(cameraEnhancer);
      ```
    > The image source in our case is a [CameraEnhancer](https://www.dynamsoft.com/camera-enhancer/docs/web/programming/javascript/user-guide/index.html) object created with `Dynamsoft.DCE.CameraEnhancer.createInstance(cameraView)`
  - **Coordinate Image-Processing Tasks**
    - The coordination happens behind the scenes. `cvRouter` starts the process by specifying a preset template "ReadSingleBarcode" in the method `startCapturing()`.
      ```js
      cvRouter.startCapturing("ReadSingleBarcode");
      ```
  - **Dispatch Results to Listening Objects**
    - The processing results are returned through the [CapturedResultReceiver](https://www.dynamsoft.com/capture-vision/docs/core/architecture/output.html#captured-result-receiver?lang=js) interface. The `CapturedResultReceiver` object is registered to `cvRouter` via the method `addResultReceiver()`. For more information, please check out [Register a result receiver](#register-a-result-receiver).
      ```js
      cvRouter.addResultReceiver({/*The-CapturedResultReceiver-Object"*/});
      ```
    - Also note that reading from video is extremely fast and there could be many duplicate results. We can use a [filter](#filter-the-results-important) with result deduplication enabled to filter out the duplicate results. The object is registered to `cvRouter` via the method `addResultFilter()`.
      ```js
      cvRouter.addResultFilter(filter);
      ```

> Read more on [Capture Vision Router](https://www.dynamsoft.com/capture-vision/docs/core/architecture/#capture-vision-router).

### Run the example

You can run the example deployed to [the Dynamsoft Demo Server](https://demo.dynamsoft.com/Samples/DBR/JS/hello-world/hello-world.html?ver=10.2.10&utm_source=guide) or test it with [JSFiddle code editor](https://jsfiddle.net/DynamsoftTeam/csm2f9wb/). 

You will be asked to allow access to your camera, after which the video will be displayed on the page. After that, you can point the camera at a barcode to read it.

When a barcode is decoded, you will see the result text show up under the video and the barcode location will be highlighted in the video feed.

Alternatively, you can test locally by copying and pasting the code shown above into a local file (e.g. "hello-world.html") and opening it in your browser.

*Note*:

If you open the web page as `file:///` or `http://` , the camera may not work correctly because the [MediaDevices: getUserMedia()](https://developer.mozilla.org/en-US/docs/Web/API/MediaDevices/getUserMedia) method only works in secure contexts (HTTPS), in some or all supporting browsers.

To make sure your web application can access the camera, please configure your web server to support HTTPS. The following links may help.

1. NGINX: [Configuring HTTPS servers](https://nginx.org/en/docs/http/configuring_https_servers.html)
2. IIS: [How to create a Self Signed Certificate in IIS](https://aboutssl.org/how-to-create-a-self-signed-certificate-in-iis/)
3. Tomcat: [Setting Up SSL on Tomcat in 5 minutes](https://dzone.com/articles/setting-ssl-tomcat-5-minutes)
4. Node.js: [npm tls](https://nodejs.org/docs/v0.4.1/api/tls.html)

If the test doesn't go as expected, you can [contact us](https://www.dynamsoft.com/company/contact/?ver=10.2.10&utm_source=guide&product=dbr&package=js).

## Building your own page

### Include the SDK

To utilize the SDK, the initial step involves including the corresponding resource files:

* `core.js` encompasses common classes, interfaces, and enumerations shared across all Dynamsoft SDKs.
* `license.js` introduces the `LicenseManager` class, which manages the licensing for all Dynamsoft SDKs.
* `utility.js` encompasses auxiliary classes shared among all Dynamsoft SDKs.
* `dbr.js` defines interfaces and enumerations tailored to the barcode reader module.
* `cvr.js` introduces the `CaptureVisionRouter` class, which governs the entire image processing workflow.
* `dce.js` comprises classes that offer camera support and basic user interface functionalities.

To simplify things, starting from version 10.0.21, we introduced `dbr.bundle.js`, which combines all six of the above files. In the following chapters, we will use `dbr.bundle.js`.

#### Use a public CDN

The simplest way to include the SDK is to use either the [jsDelivr](https://jsdelivr.com/) or [UNPKG](https://unpkg.com/) CDN. The "hello world" example above uses **jsDelivr**.

- jsDelivr

  ```html
  <script src="https://cdn.jsdelivr.net/npm/dynamsoft-barcode-reader-bundle@10.2.1000/dist/dbr.bundle.js"></script>
  ```

- UNPKG

  ```html
  <script src="https://unpkg.com/dynamsoft-barcode-reader-bundle@10.2.1000/dist/dbr.bundle.js"></script>
  ```

- In some rare cases (such as some restricted areas), you might not be able to access the CDN. If this happens, you can use the following files for the test.

  ```html
  <script src="https://download2.dynamsoft.com/packages/dynamsoft-barcode-reader-bundle@10.2.1000/dist/dbr.bundle.js"></script>
  ```

  However, please **DO NOT** use `download2.dynamsoft.com` resources in a production application as they are for temporary testing purposes only. Instead, you can try hosting the SDK yourself.

- In frameworks like React and Vue, you may want to add the package as a dependency.

  ```sh
  npm i dynamsoft-barcode-reader-bundle@10.2.1000 -E
  # or
  yarn add dynamsoft-barcode-reader-bundle@10.2.1000 -E
  ```

  NOTE that in frameworks, you need to [specify the engineResourcePaths](#specify-the-location-of-the-engine-files-optional).

#### Host the SDK yourself (optional)

Besides using the public CDN, you can also download the SDK and host its files on your own server or a commercial CDN before including it in your application.

There are two options for downloading the SDK, and the usage for each is slightly different

- From the website

  [Download Dynamsoft Barcode Reader JavaScript Package](https://www.dynamsoft.com/barcode-reader/downloads/?ver=10.2.10&utm_source=guide&product=dbr&package=js)

  The resources are located at path `dynamsoft/distributables/<pkg>@<version>`, you can typically include it like this:

  ```html
  <script src="dynamsoft/distributables/dynamsoft-barcode-reader-bundle@10.2.1000/dist/dbr.bundle.js"></script>
  ```

- npm

  ```sh
  npm i dynamsoft-barcode-reader-bundle@10.2.1000 -E
  # Compared with using CDN, you need to set up more resources.
  npm i dynamsoft-capture-vision-std@1.2.10 -E
  npm i dynamsoft-image-processing@2.2.30 -E
  ```

  The resources are located at the path `node_modules/<pkg>`, without `@<version>`, so the script would be like:

  ```html
  <script src="node_modules/dynamsoft-barcode-reader-bundle/dist/dbr.bundle.js"></script>
  ```
  
  Since the version tags (`@<version>`) are missing, you need to [specify the engineResourcePaths](#specify-the-location-of-the-engine-files-optional) so that the SDK can find the resources correctly.

  > To avoid confusion, we suggest renaming "node_modules" or moving "dynamsoft-" packages elsewhere for self-hosting, as "node_modules" is reserved for Node.js dependencies.

*Note*:

* Certain legacy web application servers may lack support for the `application/wasm` mimetype for .wasm files. To address this, you have two options:
  1. Upgrade your web application server to one that supports the `application/wasm` mimetype.
  2. Manually define the mimetype on your server. You can refer to the following resources for guidance:
     1. [Apache](https://developer.mozilla.org/en-US/docs/Learn/Server-side/Apache_Configuration_htaccess#media_types_and_character_encodings)
     2. [IIS](https://docs.microsoft.com/en-us/iis/configuration/system.webserver/staticcontent/mimemap)
     3. [Nginx](https://www.nginx.com/resources/wiki/start/topics/examples/full/#mime-types)

* To work properly, the SDK requires a few engine files, which are relatively large and may take quite a few seconds to download. We recommend that you set a longer cache time for these engine files, to maximize the performance of your web application.

  ```cmd
  Cache-Control: max-age=31536000
  ```

  Reference: [Cache-Control](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Cache-Control).

### Prepare the SDK

Before using the SDK, you need to configure a few things.

#### Specify the license

To enable the SDK's functionality, you must provide a valid license. Utilize the API function initLicense to set your license key.

```javascript
Dynamsoft.License.LicenseManager.initLicense("DLS2eyJvcmdhbml6YXRpb25JRCI6IjIwMDAwMSJ9");
```

As previously stated, the key "DLS2eyJvcmdhbml6YXRpb25JRCI6IjIwMDAwMSJ9" serves as a test license valid for 24 hours, applicable to any newly authorized browser. To test the SDK further, you can request a 30-day free trial license via the <a href="https://www.dynamsoft.com/customer/license/trialLicense?ver=10.2.10&utm_source=guide&product=dbr&package=js" target="_blank">Request a Trial License</a> link.

> Upon registering a Dynamsoft account and obtaining the SDK package from the official website, Dynamsoft will automatically create a 30-day free trial license and embed the corresponding license key into all the provided SDK samples.

#### Specify the location of the "engine" files (optional)

This is usually only required with frameworks like Angular or React, etc. where the referenced JavaScript files such as `cvr.js`, `dbr.js` are compiled into another file.

The purpose is to tell the SDK where to find the engine files (\*.worker.js, \*.wasm.js and \*.wasm, etc.). The API is called `Dynamsoft.Core.CoreModule.engineResourcePaths`:

```javascript
//The following code uses the jsDelivr CDN, feel free to change it to your own location of these files
Object.assign(Dynamsoft.Core.CoreModule.engineResourcePaths, {
  std: "https://cdn.jsdelivr.net/npm/dynamsoft-capture-vision-std@1.2.10/dist/",
  dip: "https://cdn.jsdelivr.net/npm/dynamsoft-image-processing@2.2.30/dist/",
  core: "https://cdn.jsdelivr.net/npm/dynamsoft-core@3.2.30/dist/",
  license: "https://cdn.jsdelivr.net/npm/dynamsoft-license@3.2.21/dist/",
  cvr: "https://cdn.jsdelivr.net/npm/dynamsoft-capture-vision-router@2.2.30/dist/",
  dbr: "https://cdn.jsdelivr.net/npm/dynamsoft-barcode-reader@10.2.10/dist/",
  dce: "https://cdn.jsdelivr.net/npm/dynamsoft-camera-enhancer@4.0.3/dist/"
});
```

### Set up and start image processing

#### Preload the module

The image processing logic is encapsulated within .wasm library files, and these files may require some time for downloading. To enhance the speed, we advise utilizing the following method to preload the libraries.

```js
// Preload the .wasm files
await Dynamsoft.Core.CoreModule.loadWasm(["dbr"]);
```

#### Create a CaptureVisionRouter object

To use the SDK, we first create a `CaptureVisionRouter` object.

```javascript
Dynamsoft.License.LicenseManager.initLicense("DLS2eyJvcmdhbml6YXRpb25JRCI6IjIwMDAwMSJ9");

let cvRouter = null;
try {
    cvRouter = await Dynamsoft.CVR.CaptureVisionRouter.createInstance();
} catch (ex) {
    console.error(ex);
}
```

*Tip*:

When creating a `CaptureVisionRouter` object within a function which may be called more than once, it's best to use a "helper" variable to avoid double creation such as `pCvRouter` in the following code:

```javascript
Dynamsoft.License.LicenseManager.initLicense("DLS2eyJvcmdhbml6YXRpb25JRCI6IjIwMDAwMSJ9");

let pCvRouter = null; // The helper variable which is a promise of cvRouter
let cvRouter = null;

document.getElementById('btn-scan').addEventListener('click', async () => {
    try {
        cvRouter = await (pCvRouter = pCvRouter || Dynamsoft.CVR.CaptureVisionRouter.createInstance());
    } catch (ex) {
        console.error(ex);
    }
});
```

#### Connect an image source

The `CaptureVisionRouter` object, denoted as `cvRouter`, is responsible for handling images provided by an image source. In our scenario, we aim to detect barcodes directly from a live video stream. To facilitate this, we initialize a `CameraEnhancer` object, identified as `cameraEnhancer`, which is specifically designed to capture image frames from the video feed and subsequently forward them to `cvRouter`.

To enable video streaming on the webpage, we create a `CameraView` object referred to as `cameraView`, which is then passed to `cameraEnhancer`, and its content is displayed on the webpage.

```html
<div id="camera-view-container" style="width: 100%; height: 100vh"></div>
```

```javascript
let cameraView = await Dynamsoft.DCE.CameraView.createInstance();
let cameraEnhancer = await Dynamsoft.DCE.CameraEnhancer.createInstance(cameraView);
document.querySelector("#camera-view-container").append(cameraView.getUIElement());
cvRouter.setInput(cameraEnhancer);
```

#### Register a result receiver

Once the image processing is complete, the results are sent to all the registered `CapturedResultReceiver` objects. Each `CapturedResultReceiver` object may encompass one or multiple callback functions associated with various result types. In our particular case, our focus is on identifying barcodes within the images, so it's sufficient to define the callback function `onDecodedBarcodesReceived`:

```javascript
const resultsContainer = document.querySelector("#results");
const resultReceiver = new Dynamsoft.CVR.CapturedResultReceiver();
resultReceiver.onDecodedBarcodesReceived = (result) => {
  if (result.barcodeResultItems.length > 0) {
    resultsContainer.textContent = '';
    for (let item of result.barcodeResultItems) {
      // In this example, the barcode results are displayed on the page below the video.
      resultsContainer.textContent += `${item.formatString}: ${item.text}\n\n`;
    }
  }
};
cvRouter.addResultReceiver(resultReceiver);
```

You can also write code like this. It is the same.

```javascript
const resultsContainer = document.querySelector("#results");
cvRouter.addResultReceiver({ onDecodedBarcodesReceived: (result) => {
  if (result.barcodeResultItems.length > 0) {
    resultsContainer.textContent = '';
    for (let item of result.barcodeResultItems) {
      // In this example, the barcode results are displayed on the page below the video.
      resultsContainer.textContent += `${item.formatString}: ${item.text}\n\n`;
    }
  }
}});
```

Check out [CapturedResultReceiver](https://www.dynamsoft.com/capture-vision/docs/web/programming/javascript/api-reference/capture-vision-router/captured-result-receiver.html) for more information.

#### Start the process

With the setup now complete, we can proceed to process the images in two straightforward steps:

1. Initiate the image source to commence image acquisition. In our scenario, we invoke the `open()` method on `cameraEnhancer` to initiate video streaming and simultaneously initiate the collection of images. These collected images will be dispatched to `cvRouter` as per its request.
2. Define a preset template to commence image processing. In our case, we utilize the "ReadSingleBarcode" template, specifically tailored for processing images containing a single barcode.

```javascript
await cameraEnhancer.open();
await cvRouter.startCapturing("ReadSingleBarcode");
```

*Note*:

* `cvRouter` is engineered to consistently request images from the image source.
* Various preset templates are at your disposal for barcode reading:

| Template Name                  | Function Description                                           |
| ------------------------------ | -------------------------------------------------------------- |
| **ReadBarcodes_Default**       | Scans a single barcode.                                        |
| **ReadSingleBarcode**          | Quickly scans a single barcode.                                |
| **ReadBarcodes_SpeedFirst**    | Prioritizes speed in scanning multiple barcodes.               |
| **ReadBarcodes_ReadRateFirst** | Maximizes the number of barcodes read.                         |
| **ReadBarcodes_Balance**       | Balances speed and quantity in reading multiple barcodes.      |
| **ReadDenseBarcodes**          | Specialized in reading barcodes with high information density. |
| **ReadDistantBarcodes**        | Capable of reading barcodes from extended distances.           |

Read more on the [preset CaptureVisionTemplates](https://www.dynamsoft.com/capture-vision/docs/web/programming/javascript/api-reference/capture-vision-router/preset-templates.html).

### Customize the process

#### Adjust the preset template settings

When making adjustments to some basic tasks, we often only need to modify [SimplifiedCaptureVisionSettings](https://www.dynamsoft.com/capture-vision/docs/web/programming/javascript/api-reference/capture-vision-router/interfaces/simplified-capture-vision-settings.html).

##### Change barcode settings

The preset templates can be updated to meet different requirements. For example, the following code limits the barcode format to QR code.

```javascript
let settings = await cvRouter.getSimplifiedSettings("ReadSingleBarcode");
settings.barcodeSettings.barcodeFormatIds =
  Dynamsoft.DBR.EnumBarcodeFormat.BF_QR_CODE;
await cvRouter.updateSettings("ReadSingleBarcode", settings);
await cvRouter.startCapturing("ReadSingleBarcode");
```

For a list of adjustable barcode settings, check out [SimplifiedBarcodeReaderSettings](https://www.dynamsoft.com/barcode-reader/docs/web/programming/javascript/api-reference/interfaces/simplified-barcode-reader-settings.html).

##### Retrieve the original image

Additionally, we have the option to modify the template to retrieve the original image containing the barcode.

```javascript
let settings = await cvRouter.getSimplifiedSettings("ReadSingleBarcode");
settings.capturedResultItemTypes |= 
  Dynamsoft.Core.EnumCapturedResultItemType.CRIT_ORIGINAL_IMAGE;
await cvRouter.updateSettings("ReadSingleBarcode", settings);
await cvRouter.startCapturing("ReadSingleBarcode");
```

Limit the barcode format to QR code, and retrieve the original image containing the barcode, at the same time.

```javascript
let settings = await cvRouter.getSimplifiedSettings("ReadSingleBarcode");
settings.capturedResultItemTypes = 
  Dynamsoft.DBR.EnumBarcodeFormat.BF_QR_CODE |
  Dynamsoft.Core.EnumCapturedResultItemType.CRIT_ORIGINAL_IMAGE;
await cvRouter.updateSettings("ReadSingleBarcode", settings);
await cvRouter.startCapturing("ReadSingleBarcode");
```

Please be aware that it is necessary to update the `CapturedResultReceiver` object to obtain the original image. For instance:

```javascript
const EnumCRIT = Dynamsoft.Core.EnumCapturedResultItemType;
resultReceiver.onCapturedResultReceived = (result) => {
  let barcodes = result.items.filter(item => item.type === EnumCRIT.CRIT_BARCODE);
  if (barcodes.length > 0) {
    // Use a filter to get the image on which barcodes are found.
    let image = result.items.filter(
      item => item.type === EnumCRIT.CRIT_ORIGINAL_IMAGE
    )[0].imageData;
  }
};
```

##### Change reading frequency to save power

The SDK is initially configured to process images sequentially without any breaks. Although this setup maximizes performance, it can lead to elevated power consumption, potentially causing the device to overheat. In many cases, it's possible to reduce the reading speed while still satisfying business requirements. The following code snippet illustrates how to adjust the SDK to process an image every 500 milliseconds:

> Please bear in mind that in the following code, if an image's processing time is shorter than 500 milliseconds, the SDK will wait for the full 500 milliseconds before proceeding to process the next image. Conversely, if an image's processing time exceeds 500 milliseconds, the subsequent image will be processed immediately upon completion.

```javascript
let settings = await cvRouter.getSimplifiedSettings("ReadSingleBarcode");
settings.minImageCaptureInterval = 500;
await cvRouter.updateSettings("ReadSingleBarcode", settings);
await cvRouter.startCapturing("ReadSingleBarcode");
```

##### Specify a scan region

We can specify a scan region to allow the SDK to process only part of the image, improving processing speed. The code snippet below demonstrates how to do this using the `cameraEnhancer` image source.

```javascript
cameraEnhancer = await Dynamsoft.DCE.CameraEnhancer.createInstance(cameraView);
// In this example, we set the scan region to cover the central 25% of the image.
cameraEnhancer.setScanRegion({
  x: 25,
  y: 25,
  width: 50,
  height: 50,
  isMeasuredInPercentage: true,
});
```

*Note*:

1. By configuring the region at the image source, images are cropped before processing, removing the need to adjust any further processing settings.
2. `cameraEnhancer` enhances interactivity by overlaying a mask on the video, clearly marking the scanning region.

*See Also*:

[CameraEnhancer::setScanRegion](https://www.dynamsoft.com/camera-enhancer/docs/web/programming/javascript/api-reference/acquisition.html#setscanregion)

<!-- Since DCE is always used, no need to use this approach


You can use the parameter `roi` (region of interest) together with the parameter `roiMeasuredInPercentage` to configure the SDK to only read a specific region on the image frames. For example, the following code limits the reading in the center 25%( = 50% * 50%) of the image frames:

```javascript
let settings = await cvRouter.getSimplifiedSettings("ReadSingleBarcode");
settings.roiMeasuredInPercentage = true;
settings.roi.points = [
  { x: 25, y: 25 },
  { x: 75, y: 25 },
  { x: 75, y: 75 },
  { x: 25, y: 75 },
];
await cvRouter.updateSettings("ReadSingleBarcode", settings);
await cvRouter.startCapturing("ReadSingleBarcode");
``` -->


<!--
* Specify the maximum time allowed for processing each image

You can set the maximum time allowed for processing a single image with the property `timeout`.

> Please be aware that the SDK will cease processing an image if its processing time exceeds the duration specified by the `timeout` parameter. It should not be confused with the previously discussed parameter, `minImageCaptureInterval`.

```javascript
let settings = await cvRouter.getSimplifiedSettings("ReadSingleBarcode");
settings.timeout = 500;
await cvRouter.updateSettings("ReadSingleBarcode", settings);
await cvRouter.startCapturing("ReadSingleBarcode");
```
-->

#### Edit the preset templates directly

The preset templates have many more settings that can be customized to suit your use case best. If you [download the SDK from Dynamsoft website](https://www.dynamsoft.com/barcode-reader/downloads/1000003-confirmation/), you can find the templates under

* "/dynamsoft-barcode-reader-js-10.2.10/dynamsoft/resources/barcode-reader/templates/"

Upon completing the template editing, you can invoke the `initSettings` method and provide it with the template path as an argument.

```javascript
await cvRouter.initSettings("PATH-TO-THE-FILE"); // E.g. "https://your-website/ReadSingleBarcode.json")
await cvRouter.startCapturing("ReadSingleBarcode"); // Make sure the name matches one of the CaptureVisionTemplates in the template JSON file.
```

#### Filter the results (Important)

While processing video frames, it's common for the same barcode to be detected multiple times. To enhance the user experience, we can use [MultiFrameResultCrossFilter](https://www.dynamsoft.com/capture-vision/docs/web/programming/javascript/api-reference/utility/multi-frame-result-cross-filter.html) object, having two options currently at our disposal:

##### Option 1: Verify results across multiple frames

```js
let filter = new Dynamsoft.Utility.MultiFrameResultCrossFilter();
filter.enableResultCrossVerification("barcode", true);
await cvRouter.addResultFilter(filter);
```

*Note*:

* `enableResultCrossVerification` was designed to cross-validate the outcomes across various frames in a video streaming scenario, enhancing the reliability of the final results. This validation is particularly crucial for barcodes with limited error correction capabilities, such as 1D codes.

##### Option 2: Eliminate redundant results detected within a short time frame

```js
let filter = new Dynamsoft.Utility.MultiFrameResultCrossFilter();
filter.enableResultDeduplication("barcode", true);
await cvRouter.addResultFilter(filter);
```

*Note*:

* `enableResultDeduplication` was designed to prevent high usage in video streaming scenarios, addressing the repetitive processing of the same code within a short period of time.

Initially, the filter is set to forget a result 3 seconds after it is first received. During this time frame, if an identical result appears, it is ignored.

> It's important to know that in version 9.x or earlier, the occurrence of an identical result would reset the timer, thus reinitiating the 3-second count at that point. However, in version 10.2.10 and later, an identical result no longer resets the timer but is instead disregarded, and the duration count continues uninterrupted.

Under certain circumstances, this duration can be extended with the method `setDuplicateForgetTime()`.

```js
let filter = new Dynamsoft.Utility.MultiFrameResultCrossFilter();
filter.setDuplicateForgetTime(5000); // Extend the duration to 5 seconds.
await cvRouter.addResultFilter(filter);
```

You can also enable both options at the same time:

```js
let filter = new Dynamsoft.Utility.MultiFrameResultCrossFilter();
filter.enableResultCrossVerification("barcode", true);
filter.enableResultDeduplication("barcode", true);
filter.setDuplicateForgetTime(5000);
await cvRouter.addResultFilter(filter);
```

#### Add feedback

When a barcode is detected within the video stream, its position is immediately displayed within the video. Furthermore, utilizing the "Dynamsoft Camera Enhancer" SDK, we can introduce feedback mechanisms, such as emitting a "beep" sound or triggering a "vibration".

The following code snippet adds a "beep" sound for when a barcode is found:

```js
const resultReceiver = new Dynamsoft.CVR.CapturedResultReceiver();
resultReceiver.onDecodedBarcodesReceived = (result) => {
  if (result.barcodeResultItems.length > 0) {
    Dynamsoft.DCE.Feedback.beep();
  }
};
cvRouter.addResultReceiver(resultReceiver);
```

### Customize the UI

The UI is part of the auxiliary SDK "Dynamsoft Camera Enhancer", read more on how to [customize the UI](https://www.dynamsoft.com/camera-enhancer/docs/web/programming/javascript/user-guide/index.html#customize-the-ui).

## API Documentation

You can check out the detailed documentation about the APIs of the SDK at
[https://www.dynamsoft.com/barcode-reader/docs/web/programming/javascript/api-reference/?ver=10.2.10](https://www.dynamsoft.com/barcode-reader/docs/web/programming/javascript/api-reference/?ver=10.2.10).

## System Requirements

DBR requires the following features to work:

- Secure context (HTTPS deployment)

  When deploying your application / website for production, make sure to serve it via a secure HTTPS connection. This is required for two reasons
  
  - Access to the camera video stream is only granted in a security context. Most browsers impose this restriction.
  > Some browsers like Chrome may grant the access for `http://127.0.0.1` and `http://localhost` or even for pages opened directly from the local disk (`file:///...`). This can be helpful for temporary development and test.
  
  - Dynamsoft License requires a secure context to work.

- `WebAssembly`, `Blob`, `URL`/`createObjectURL`, `Web Workers`

  The above four features are required for the SDK to work.

- `MediaDevices`/`getUserMedia`

  This API is required for in-browser video streaming.

- `getSettings`

  This API inspects the video input which is a `MediaStreamTrack` object about its constrainable properties.

The following table is a list of supported browsers based on the above requirements:

  | Browser Name |     Version      |
  | :----------: | :--------------: |
  |    Chrome    | v78+<sup>1</sup> |
  |   Firefox    | v62+<sup>1</sup> |
  |     Edge     |       v79+       |
  |    Safari    |       v14+       |

  <sup>1</sup> devices running iOS needs to be on iOS 14.3+ for camera video streaming to work in Chrome, Firefox or other Apps using webviews.

Apart from the browsers, the operating systems may impose some limitations of their own that could restrict the use of the SDK. Browser compatibility ultimately depends on whether the browser on that particular operating system supports the features listed above.

## How to Upgrade

If you want to upgrade the SDK from an old version to a newer one, please see [how to upgrade](https://www.dynamsoft.com/barcode-reader/docs/web/programming/javascript/upgrade-guide/index.html?ver=10.2.10&utm_source=guide).

## Release Notes

Learn about what are included in each release at [https://www.dynamsoft.com/barcode-reader/docs/web/programming/javascript/release-notes/index.html](https://www.dynamsoft.com/barcode-reader/docs/web/programming/javascript/release-notes/index.html?ver=10.2.10&utm_source=guide).

## Next Steps

Now that you have got the SDK integrated, you can choose to move forward in the following directions

1. Learn how to [Use in Framework](https://www.dynamsoft.com/barcode-reader/docs/web/programming/javascript/user-guide/use-in-framework.html)
2. Check out the [Official Samples and Demo](https://www.dynamsoft.com/barcode-reader/docs/web/programming/javascript/samples-demos/index.html?ver=10.2.10)
3. Learn about the [APIs of the SDK](https://www.dynamsoft.com/barcode-reader/docs/web/programming/javascript/api-reference/index.html?ver=10.2.10)