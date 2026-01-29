# open-weather-fetch

This is a JSON file format for weather data to be downloaded in, to be used by
various weather clients, primarily on GNU/Linux systems.

The project offers a backend/frontend split, making it so the weather backends
periodically save updated weather data to a file. Then, the various weather
clients one desires to use can all have recent weather information without
having to make requests themselves, and allowing the user to choose their
desired weather source independently of the display software.

Weather data is stored in JSON, in `~/.local/share/weather/data/`. To see the
weather JSON spec, refer to `data_file_spec.md` in this repository.

In that directory, a `data.json` file is the main weather file. In the future,
it will be possible to have a subdirectory `locations` with more weather files
for other locations, keeping `data.json` for the current one. That is, a small
weather client such as a panel applet can read just `data.json`, whereas a
windowed weather app might want to read all cities.

## Downloading weather data

There will be a systemd user unit, but even without that, you can run one of
the backends periodically like this bash:

~~~bash
while true; do python fetchers/example.py [options]; sleep 10m; done
~~~

Each backend has at least the following parameters:

* `-l`, `--location`: the city name to download weather data for (required).
* `-u`, `--units`: `metric` or `imperial` to override the unit type. If not
  specified, it will try to use locale services to find the system-set one.
  Note that if you are in the USA, you should set your locale to `en_US.UTF-8`
  and not `C.UTF-8` as is common on many hand-installed distributions, if you
  want Imperial units.

If the specific backend requires an API key, there will be a `-k`, `--apikey`
parameter to specify the key.
