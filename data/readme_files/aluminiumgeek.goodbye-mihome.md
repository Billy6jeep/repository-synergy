# Goodbye MiHome

Break into API of smart home products from Xiaomi and wrap sensors data to cozy web interface.

If you like this project, you might want to buy me a cup of coffee :)  
[![](https://cloud.githubusercontent.com/assets/840753/23658304/6ac22b4c-035b-11e7-978d-79392dc65143.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_donations&business=G8NJ4AKLEZRBE&lc=US&item_name=aluminiumgeek&item_number=goodbye%2dmihome&currency_code=USD&bn=PP%2dDonationsBF%3abtn_donateCC_LG%2egif%3aNonHostedd3faee8d94717bd303200c3af9aadd01a5f55080)


### Currently supported devices

- Temperature and humidity sensor: collect data, show current value and line charts.
- Magnet (door/window close sensor): collect data, show current status, pubsub service to be used in apps.
- Gateway LED: change color, set brightness, toggle status, show current value.
- Gateway Speaker: play standard and user-defined (uploaded via MiHome app) sounds with custom volume, interrupt playing.
- Yeelight smart LED bulbs: toggle status, set brightness, set name, create scenes, manage cron jobs.

The list will expand as I receive more Xiaomi devices and make plugins for them. Feel free to write your plugins if you have other devices/sensors.

### Setup and running

1. Ensure you have Python 3, PostgreSQL, Redis installed.
2. Clone the repo
3. Create a PostgreSQL database and import `init.sql`
4. Install required python packages: `pip install -r requirements.txt`
4. Copy `config.py.example` to `config.py` and fill it with your settings
5. Run `python mihome.py` to start data collector, web application and load apps defined in `ENABLED_APPS`.  
   Additionally, run `python mihome.py shell` to start interactive intepreter (useful to test commands).


### Apps

Besides displaying sensors and devices data and change settings from the web interface, you could write some useful apps using Goodbye-MiHome. For example, you could parse your electricity supplier's website and start red LED blinking on the gateway when there's a news about upcoming power outage in your area.

Some sample apps could be found in `apps` directory.

You could enable or disable an app by changing `ENABLED_APPS` section in `config.py`

### Background images for web interface

To make web interface even better, you could put your favorite images into `web/static/img/bg/` directory. Background image changes every 5 minutes (hovewer, you could tweak the interval in js file).

![goodbye-mihome](https://user-images.githubusercontent.com/840753/29633763-60f6ea62-8858-11e7-8fc9-415f5e8daa72.jpg)
