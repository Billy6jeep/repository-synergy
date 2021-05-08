# Apple Pattern of Life Lazy Output'er (APOLLO)
* Originally presented as the first ever [Objective by the Sea](https://objectivebythesea.com/) - Mac Security Conference in 2018
* Presentation Slides: [From Apple Seeds to Apple Pie](https://github.com/mac4n6/Presentations/tree/master/From%20Apple%20Seeds%20to%20Apple%20Pie)
* Presentation Slides: [Launching APOLLO: Creating a Simple Tool for Advanced Forensic Analysis](https://github.com/mac4n6/Presentations/tree/master/LaunchingAPOLLO)

# v1.0
* Software has bugs, always ensure your data makes sense and go to the original data to verify. Test, test, test!
* Find a bug or a better query, let me know!
* Many more modules to come!
* Python 3

## Dependencies
* [SimpleKML](https://simplekml.readthedocs.io) - Copy the `simplekml` directory to the directory where apollo.py is being run from. [Download here](https://pypi.org/project/simplekml/#files)
* Depending on your python3 installation you may get a `No module named 'six` error, [you will need to install `six`](https://lmgtfy.com/?q=python3+install+six)

### On macOS 10.15 to install `six` and `simplekml` dependencies:
* `sudo easy_install pip`
* `pip3 install six`
* `pip3 install simplekml`

## Usage
`python apollo.py -o {csv, sql} -p {ios, mac, yolo} -v {8,9,10,11,12,yolo} -k <modules directory> <data directory>`

## Output Options (-o)
* `csv` - CSV
* `sql` - SQLite Database

## KMZ Output(-k)
* Outputs location coordinates to separate files based on module.
* [iOS Location Mapping with APOLLO - I Know Where You Were Today, Yesterday, Last Month, and Years Ago!](https://www.mac4n6.com/blog/2019/8/21/i-know-where-you-were-today-yesterday-last-month-and-many-years-ago)
* [iOS Location Mapping with APOLLO – Part 2: Cellular and Wi-Fi Data (locationd)](https://www.mac4n6.com/blog/2019/8/25/ios-location-mapping-with-apollo-part-2-cellular-and-wi-fi-data-locationd)

## Platform Options (-p)
* `ios`
* `mac` [Offical support coming soon!]
* `yolo` - Just parse whatever.  Use for ARTEMIS parsing.

## Version Options (-v)
* iOS `8`, `9`, `10`, `11`, `12`
* `yolo` - Just parse whatever. Use for ARTEMIS parsing.

## Getting Errors? Try This (Windows users, use eqivlent commands)
You may see that APOLLO reports back "0 databases" found when executed, most likely from CurrentPowerlog.PLSQL and locationd modules. Two common directories with databases that cause problems due to permissions (depends on how files were extracted from device):
* `/private/var/root/Library/Caches/locationd/`
* `/private/var/containers/Shared/SystemGroup/[GUID]/Library/BatteryLife`
### Fix Permissions:
* `chmod -R 755 /private/var/containers/Shared/SystemGroup/[GUID_for BatteryLife Data]/`
* `chmod -R 755 /private/var/root`

### Still not working?
* Check database permissions - Use `chmod` to give some databases with "all blank" permissions some sort of permission. (Happens with many types of physical-logical extractions.)
* Check database ownership - Use `chown` to take ownership of the files.

## To Do List
* Powerlog Gzip Files
* Database Coalescing
* MacOS-specifc modules and handling
* Visualizations
* Accept Zip file input
* Modules:
  * Screen Time
  * Additional Health modules 

## Thank You!
* Thanks to Sam Alptekin of @sjc_CyberCrimes, script is much, much faster than original.
* [Thanks to @AlexisBrignoni for Python 3 support and ARTEMIS!](https://abrignoni.blogspot.com/2019/08/artemis-android-support-for-apollo.html)

## References
* [Knowledge is Power! Using the macOS/iOS knowledgeC.db Database to Determine Precise User and Application Usage](https://www.mac4n6.com/blog/2018/8/5/knowledge-is-power-using-the-knowledgecdb-database-on-macos-and-ios-to-determine-precise-user-and-application-usage)
* [Knowledge is Power II – A Day in the Life of My iPhone using knowledgeC.db](https://www.mac4n6.com/blog/2018/9/12/knowledge-is-power-ii-a-day-in-the-life-of-my-iphone-using-knowledgecdb)
* [On the First Day of APOLLO, My True Love Gave to Me - A Python Script – An Introduction to the Apple Pattern of Life Lazy Output’er (APOLLO) Blog Series](https://www.mac4n6.com/blog/2018/12/14/on-the-first-day-of-apollo-my-true-love-gave-to-me-a-python-script-an-introduction-to-the-apple-pattern-of-life-lazy-outputer-apollo-blog-series)
* [On the Second Day of APOLLO, My True Love Gave to Me - Holiday Treats and a Trip to the Gym - A Look at iOS Health Data](https://www.mac4n6.com/blog/2018/12/15/on-the-second-day-of-apollo-my-true-love-gave-to-me-holiday-treats-and-a-trip-to-the-gym-a-look-at-ios-health-data)
* [On the Third Day of APOLLO, My True Love Gave to Me – Application Usage to Determine Who Has Been Naughty or Nice](https://www.mac4n6.com/blog/2018/12/16/on-the-third-day-of-apollo-my-true-love-gave-to-me-application-usage-to-determine-who-has-been-naughty-or-nice)
* [On the Fourth Day of APOLLO, My True Love Gave to Me – Media Analysis to Prove You Listened to “All I Want for Christmas is You” Over and Over Since Before Thanksgiving](https://www.mac4n6.com/blog/2018/12/17/on-the-fourth-day-of-apollo-my-true-love-gave-to-me-media-analysis-to-prove-you-listened-to-all-i-want-for-christmas-is-you-over-and-over-since-before-thanksgiving)
* [On the Fifth Day of APOLLO, My True Love Gave to Me – A Stocking Full of Random Junk, Some of Which Might be Useful!](https://www.mac4n6.com/blog/2018/12/18/on-the-fifth-day-of-apollo-my-true-love-gave-to-me-a-stocking-full-of-random-junk-some-of-which-might-be-useful)
* [On the Sixth Day of APOLLO, My True Love Gave to Me – Blinky Things with Buttons – Device Status Analysis](https://www.mac4n6.com/blog/2018/12/19/on-the-sixth-day-of-apollo-my-true-love-gave-to-me-blinky-things-with-buttons-device-status-analysis)
* [On the Seventh Day of APOLLO, My True Love Gave to Me – A Good Conversation – Analysis of Communications and Data Usage](https://www.mac4n6.com/blog/2018/12/20/on-the-seventh-day-of-apollo-my-true-love-gave-to-me-a-good-conversation-analysis-of-communications-and-data-usage)
* [On the Eighth Day of APOLLO, My True Love Gave to Me – A Glorious Lightshow – Analysis of Device Connections](https://www.mac4n6.com/blog/2018/12/21/on-the-eighth-day-of-apollo-my-true-love-gave-to-me-a-glorious-lightshow-analysis-of-device-connections)
* [On the Ninth Day of APOLLO, My True Love Gave to Me – A Beautiful Portrait – Analysis of the iOS Interface](https://www.mac4n6.com/blog/2018/12/22/on-the-ninth-day-of-apollo-my-true-love-gave-to-me-a-beautiful-portrait-analysis-of-the-ios-interface)
* [On the Tenth Day of APOLLO, My True Love Gave to Me – An Oddly Detailed Map of My Recent Travels – iOS Location Analysis](https://www.mac4n6.com/blog/2018/12/23/on-the-tenth-day-of-apollo-my-true-love-gave-to-me-an-oddly-detailed-map-of-my-recent-travels-ios-location-analysisk)
* [On the Eleventh Day of APOLLO, My True Love Gave to Me – An Intriguing Story – Putting it All Together: A Day in the Life of My iPhone using APOLLO](https://www.mac4n6.com/blog/2018/12/24/on-the-eleventh-day-of-apollo-my-true-love-gave-to-me-an-intriguing-story-putting-it-all-together-a-day-in-the-life-of-my-iphone-using-apollo)
* [On the Twelfth Day of APOLLO, My True Love Gave to Me – A To Do List – Twelve Planned Improvements to APOLLO](https://www.mac4n6.com/blog/2018/12/25/on-the-twelfth-day-of-apollo-my-true-love-gave-to-me-a-to-do-list-twelve-planned-improvements-to-apollo)
