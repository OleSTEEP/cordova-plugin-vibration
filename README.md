---
title: Vibration
description: Vibrate the device.
---
<!--
# license: Licensed to the Apache Software Foundation (ASF) under one
#         or more contributor license agreements.  See the NOTICE file
#         distributed with this work for additional information
#         regarding copyright ownership.  The ASF licenses this file
#         to you under the Apache License, Version 2.0 (the
#         "License"); you may not use this file except in compliance
#         with the License.  You may obtain a copy of the License at
#
#           http://www.apache.org/licenses/LICENSE-2.0
#
#         Unless required by applicable law or agreed to in writing,
#         software distributed under the License is distributed on an
#         "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
#         KIND, either express or implied.  See the License for the
#         specific language governing permissions and limitations
#         under the License.
-->

|AppVeyor|Travis CI|
|:-:|:-:|
|[![Build status](https://ci.appveyor.com/api/projects/status/github/apache/cordova-plugin-vibration?branch=master)](https://ci.appveyor.com/project/ApacheSoftwareFoundation/cordova-plugin-vibration)|[![Build Status](https://travis-ci.org/apache/cordova-plugin-vibration.svg?branch=master)](https://travis-ci.org/apache/cordova-plugin-vibration)|

# cordova-plugin-vibration

This plugin aligns with the W3C vibration specification http://www.w3.org/TR/vibration/

This plugin provides a way to vibrate the device.

This plugin defines global objects including `navigator.vibrate`.

Although in the global scope, they are not available until after the `deviceready` event.

    document.addEventListener("deviceready", onDeviceReady, false);
    function onDeviceReady() {
        console.log(navigator.vibrate);
    }

:warning: Report issues on the [Apache Cordova issue tracker](https://issues.apache.org/jira/issues/?jql=project%20%3D%20CB%20AND%20status%20in%20%28Open%2C%20%22In%20Progress%22%2C%20Reopened%29%20AND%20resolution%20%3D%20Unresolved%20AND%20component%20%3D%20%22Plugin%20Vibration%22%20ORDER%20BY%20priority%20DESC%2C%20summary%20ASC%2C%20updatedDate%20DESC)


## Installation

    cordova plugin add cordova-plugin-vibration

## Supported Platforms

navigator.vibrate,<br />
navigator.notification.vibrate
- Amazon Fire OS
- Android
- BlackBerry 10
- Firefox OS
- iOS
- Windows Phone 7 and 8
- Windows (Windows Phone 8.1 devices only)


The Android webview (API level 19 and up) supports the [W3C Vibration API](https://www.w3.org/TR/vibration/) natively and therefore, the Android specific implementation of this plugin has been dropped.

## vibrate

This function has three different functionalities based on parameters passed to it.

### Standard vibrate

Vibrates the device for a given amount of time.

    navigator.vibrate(time)

or

    navigator.vibrate([time])


-__time__: Milliseconds to vibrate the device. _(Number)_

#### Example

    // Vibrate for 3 seconds
    navigator.vibrate(3000);

    // Vibrate for 3 seconds
    navigator.vibrate([3000]);

#### iOS Quirks

- __time__: Ignores the specified time and vibrates for a pre-set amount of time.

    navigator.vibrate(3000); // 3000 is ignored

#### Windows and Blackberry Quirks

- __time__: Max time is 5000ms (5s) and min time is 1ms

    navigator.vibrate(8000); // will be truncated to 5000

### Vibrate with a pattern (Android and Windows only)
Vibrates the device with a given pattern

    navigator.vibrate(pattern);

- __pattern__: Sequence of durations (in milliseconds) for which to turn on or off the vibrator. _(Array of Numbers)_

#### Example

    // Vibrate for 1 second
    // Wait for 1 second
    // Vibrate for 3 seconds
    // Wait for 1 second
    // Vibrate for 5 seconds
    navigator.vibrate([1000, 1000, 3000, 1000, 5000]);

#### Windows Phone 8 Quirks

- vibrate(pattern) falls back on vibrate with default duration

### Cancel vibration (not supported in iOS)

Immediately cancels any currently running vibration.

    navigator.vibrate(0)

or

    navigator.vibrate([])

or

    navigator.vibrate([0])

Passing in a parameter of 0, an empty array, or an array with one element of value 0 will cancel any vibrations.




