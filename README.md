# Weather-Delta-API
Simple weather API for Android

This class is meant to be a simple way for Android apps to interact with <a href="https://play.google.com/store/apps/details?id=com.felkertech.n.weatherdelta">Weather Delta</a> for the sake of
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

## Usage
First, add WeatherBroadcasterUtils.java to your app. This will take care of a lot of boilerplate code automatically, giving you simple methods to call.

You will need to create add an intent filter in your manifest to receive weather messages:

    <service
          android:name=".services.WeatherReceiver"
          android:enabled="true"
          android:exported="true" >
          <intent-filter>
              <action android:name="com.felkertech.n.weatherdelta.CURRENT_WEATHER"/>
          </intent-filter>
      </service>

This service will catch any calls from Weather Delta whenever the weather is refreshed by the user.

### Request Most Recent Data
To manually request weather data:

    startService(WeatherBroadcasterUtils.getWeatherRequest());

This will tell Weather Delta to send out a new broadcast. 

### Check if App is Installed
Weather Delta may not be installed on the user's device, and so the previous request may be ignored. To check:

    WeatherBroadcasterUtils.isAppInstalled(mContext);
  
### Retrieving Data
When you get your data from the receiver, instantiate an object of the class `WeatherBroadcasterUtils` using that intent.

    WeatherBroadcasterUtils wbu = new WeatherBroadcasterUtils(intent);

From here, you can call a variety of methods to get weather data.

| Method | Return | Description |
| :---   | :---:  | ---: |
| `isMetric()` | `boolean` | Returns the unit system for the data |
| `getLastCheckedTime()` | `long` | Returns the time in milliseconds since the Unix Epoch that the data was refreshed |
| `getApiVersion()` | `int` | Returns the app version installed on the user's device |
| `getCurrentRainProbability()` | `int` | Retrieves the current forecasted probability of rain (out of 100) |
| `getCurrentRainIntensity()` | `String` | Retrieves the forecasted strongest intensity of precipitation |
| `getCurrentRainType()` | `String` | Retrieves the forecasted type of precipitation |
| `getCurrentRainSummary()` | `String` | Retrieves a forecast for today's precipitation |
| `getCurrentTemperature()` | `int` | Retrieves the current temperature at the given location in the user's specified units |
| `getCurrentTemperatureSummary()` | `String` | Retrieves a forecast for today's temperature |

