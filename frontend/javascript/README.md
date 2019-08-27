<p>
  <img src="https://inspetor-assets.s3-sa-east-1.amazonaws.com/images/inspetor-logo.png" width="200" height="40" alt="Inspetor Logo">
</p>

# Inspetor Antifraud
Antrifraud Inspetor library for Javascript (browser).

## Description
Inspetor is an product developed to help your company to avoid fraudulent transactions. This README file should help you to integrate the Inspetor Javascript library into your product with a couple steps. 

P.S.: the library was made in Typescript, but all the code you will see here will be in Javascript.

## How to use
The Inspetor Javascript Library can be installed through [npm](https://npmjs.com) or by a `<script>` (Global Variable) tag.

**We recomend** you to use the `<script>` tag (Global Variable) since this is a browser library.

### Npm Method
First, install it:
```
npm install inspetor
```
After that you can import the library as usual:
```
import inspetor from 'inspetor'
```
or using `require` 
```
const inspetor = require('inspetor')
```

PS: If you are using Browserify check on how to make our variable global

### Script Tag (Global Variable)
You can also use the latest release from our CDN and import the build directly in your HTML:
```
<script src="https://files.useinspetor.com/inspetor-js/inspetor.min.js" />
```
The library will be available as the global variable `inspetor`.

## API Docs
You can find an more in depth documentation about our frontend libraries [here](https://inspetor.github.io/docs-frontend).

When using our Javascript library you will notice that we will import another `<script>` (inspetor-asset.min.js) that we require for our library.

Before using any of the funtions in the library you need to provide authentication details which will be used through library calls.

### Library setup
All the access to the Inspetor functions is made through our `sharedInstance` that is available by calling the `inspetor.sharedInstance()`. But before you can call any of our collection functions you need to configure the library. To do that all you need is the following code:

Be advised, that this function can throw an exception if you pass invalids (empty strings or not in the format required) appId or/and trackerName.

```
  inspetor.sharedInstance().setup("appId", "trackerName", false, true);
```

The parameters passed are the following, in order:

Parameter | Required | Type | Description 
--------- | -------- | ---- | ----------- 
appId           | Yes | String  | An unique identifier that the Inspetor Team will provide to you
trackerName     | Yes | String  | A name that will help us to find your data in our database and we'll provide you with a couple of them
requestLocation | Yes | Boolean | If set to `true` we will ask for the user permission
devEnv          | No  | Boolean | Indicates that your are testing the library (development enviroment), meaning that data is not ready for production. It's set to `false` by default.

### Library Calls
If you've already read the [general Inspetor files](https://inspetor.github.io/docs-frontend), you should be aware of all of Inspetor requests and collection functions.

Here we will show you some details to be aware in you are calling the Inspetor tracking functions.

All of out *track functions* can throw exceptions, but the only exception they will through is if you forget to configure the Inspetor Library before calling one of them. Because of that the Inspetor class have a function called `isConfigured()` that returns a boolean saying if you have configured or not the Inspetor Library. We recommend that when you call any of our tracking functions you check if the Inspetor Library is configured. Here is an example on how to do that:

```
if (inspetor.sharedInstance().isConfigured()) {
    inspetor.sharedInstance().trackAccountCreation("123");
}
```

#### trackPageView
The **pageview tracking is done automatically** in the library, **everytime the user reloads the page or chanegs the state of the page**. But we do give the option to track "pseudo pageview", pageviews that do not change the page or do not alter the state (change the url of the page). You should be carefull when manually tracking pageviews since it can lead to duplicate pageview events. **We recommend that you contact the Inspetor team to get advice if you should or should not use the `trackPageView` function**. 

Here you can see an example on how the tracker is implemented.

```
if (inspetor.sharedInstance().isConfigured()) {
    inspetor.sharedInstance().trackPageView("Pseudo PageView")
}
```

### Models
If you are comming from one of our backend libraries you will notice that we do not use models in our frontend libraries. Here you just need to send us the id of the model.

## More Information
For more info you should check the [Inspetor Frontend docs](https://inspetor.github.io/docs-frontend)
