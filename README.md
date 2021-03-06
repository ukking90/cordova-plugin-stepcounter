# Cordova Step Counter Plugin

Uses the step counter service APIs introduced in Android 4.4 KitKat to, you guessed it, count the number of steps whomever is holding the device running your app takes.

## Using
Clone the plugin

    $ git clone https://github.com/texh/cordova-plugin-stepcounter.git

Create a new Cordova Project

    $ cordova create hello com.example.helloapp Hello
    
Install the plugin

    $ cd hello
    $ cordova plugin install ../cordova-plugin-stepcounter
    

Edit `www/js/index.html` and add the following code inside `onDeviceReady`

```js
    var success = function(message) {
        alert(message);
    }

    var failure = function() {
        alert("Error calling CordovaStepCounter Plugin");
    }

    // Start the step counter
    // startingOffset will be added to the total steps counted in this session.
    // ie. say you have already recorded 150 steps for a certain activity, then
    // the step counter records 50. The getStepCount method will then return 200.
    var startingOffset = 0;
    stepcounter.start(startingOffset, success, failure);

    // Stop the step counter
    stepcounter.stop(success, failure);

    // Get the amount of steps since calling start (or 0 if it hasn't been run)
    stepcounter.getStepCount(success, failure);

    // Returns true/false if Android device is running >API level 19 && has the step counter API available
    stepcounter.deviceCanCountSteps(success, failure);
```

Install Android platform

    cordova platform add android
    
Run the code

    cordova run 

## Compatibility

This will only work on Android devices running 4.4 (KitKat) or higher, and that have a step counter sensor. This includes Google's Nexus line of handsets, and potentially some others.

Use stepcounter.deviceCanCountSteps() to see if a device meets these requirements before trying to use it any further.

## Here be dragons

The quality, usefulness and functionality of this code is in no way guaranteed. This is far from production ready stuff you're looking at, and definitely has a few hairy parts that need combing over.
If you'd like to help, I'd love to hear from you!

### Outstanding issues

Android seems to randomly kill the step counter if your application is running in the background (ie. in the case of multitasking)

## More Info

For more information on setting up Cordova see [the documentation](http://cordova.apache.org/docs/en/4.0.0/guide_cli_index.md.html#The%20Command-Line%20Interface)

For more info on plugins see the [Plugin Development Guide](http://cordova.apache.org/docs/en/4.0.0/guide_hybrid_plugins_index.md.html#Plugin%20Development%20Guide)
