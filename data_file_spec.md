# weather-fetch data file specification

Produce files in JSON format, which are organised like:

* `location` (object):
  * `name`: the city name
  * `long`: longitude
  * `lat`: latitude
* `units` (object):
  * `temp` (`C`, `F`)
  * `pres` (`hPa`, `mmHg`)
  * `wind` (`m/s`, `km/h`, `mi/h`)
  * `prec` (`mm`)
  * `visi` (`m`)

And define "weather information" like this:

* `time`: the Unix time of the weather data
* `temp`: *formatted* temperature representation, with unit (`8°C`)
* `feels_like_temp`: numeric value of the perceived temperature
* `temp_value`: numeric value of temperature
* `icon_name`: freedesktop.org icon name for the weather state
* `conditions`: textual description
* `icon`: full path to a suitable icon file for the weather state
* `prec`: quantity of precipitation for the given period (for the current conditions, it is for 1 hour)
* `coverage`: percentage of cloud coverage
* `pop`: probability of precipitation
* `sunrise`: the Unix time of sunrise
* `sunset`: the Unix time of sunset
* `moonrise`: the Unix time of moonrise
* `moonset`: the Unix time of moonset
* `visi`: visibility
* `wind`: wind speed
* `wind_source`: direction in degrees of the origin of wind
* `wind_gust`: wind gust speed
* `pres`: pressure
* `dew_point`: dew point
* `fog`: percentage of fog

In the root object, put the weather information. Then, if you provide forecasts,
add a `forecast` key with a list of weather information, each with the
appropriate time.

If you don't have access to certain data, you can omit the key, or put `null` in
it.
