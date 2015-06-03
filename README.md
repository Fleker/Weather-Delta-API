# Weather-Delta-API
Simple weather API for Android

This class is meant to be a simple way for Android apps to interact with Weather Delta for the sake of
getting simple weather data in their app without having to program any complex code.

## Pros
* All of the download management is managed in the background, you don't need to code it
* There is no need to request the user's location or Internet
* Most recent data is cached, giving you data instantly, even when offline
* As Weather Delta continues to evolve, your app also improves without any extra work
* User customization is handled by the Weather Delta app, like metric and download settings,
so you don't need to rewrite the wheel
* Many weather services have prices per API call online. As the data is cached on this device,
there is no cost to you to implement this, it's merely extending data already available.
* All of the data parsing is already handled. Getting the temperature is one simple method.
There's also richer weather information in the summaries.
* l18n for weather data is already built-in
* Weather Delta is available on Android phones, tablets, TVs, and Wear. Your app can access this
API on all devices. (The Wear app currently doesn't support this API, so you'll have to get the
data from the mobile app)

## Cons
* Users will need to have Weather Delta installed on their device in order for this API to work.
Use `isAppInstalled` to check whether these APIs can be used.
