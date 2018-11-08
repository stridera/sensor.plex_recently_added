___

<h1 align="center"> :warning:  THIS IS THE DEV BRANCH!  :warning:</h1>
<h2 align="center">
May contain bugs, broken features, and should generally be avoided.</br></br>

___


# Plex Recently Added Component

Home Assistant component to feed [Upcoming Media Card](https://github.com/custom-cards/upcoming-media-card) with
Plex's recently added media.</br>
This component does not require, nor conflict with, the default Plex components.</br></br>
<link href="https://fonts.googleapis.com/css?family=Lato&subset=latin,latin-ext" rel="stylesheet"><a class="bmc-button" target="_blank" href="https://www.buymeacoffee.com/FgwNR2l"><img src="https://www.buymeacoffee.com/assets/img/BMC-btn-logo.svg" alt="Buy me a coffee"><span style="margin-left:5px">If you feel I deserve it, you can buy me a coffee</span></a></br>
</br>

## Installation:
### In it's current state, this component only works if Home Assistant and your Plex server are on the same network.
1. Install this component by copying to your `/custom_components/sensor/` folder.
2. Install the card: [Upcoming Media Card](https://github.com/custom-cards/upcoming-media-card)
3. Add the code to your `configuration.yaml` using the config options below.
4. Add the code for the card to your `ui-lovelace.yaml`. 
5. **You will need to restart after installation for the component to start working.**

### Options

| key | default | required | description
| --- | --- | --- | ---
| token | | yes | Your Plex token [(Find your Plex token)](https://support.plex.tv/articles/204059436-finding-an-authentication-token-x-plex-token/)
| server_name |  | yes | The name of your Plex server. Can be found in Plex's server settings in "General".
| ssl | false | no | Set to true if you use SSL to access Plex.
| max | 5 | no | Max number of items to show in sensor.
| download_images | true | no | Setting this to false will turn off downloading of images, but will require certain Plex settings to work seen below.
| ssl_cert | false | no | If you provide your own SSL certificate in Plex's network settings set this to true.

#### By default this addon automatically downloads images from Plex to your /www/custom-lovelace/upcoming-media-card/ directory. The directory is automatically created & only images reported in the upcoming list are downloaded. Images are small in size and are removed automatically when no longer needed.

#### If you prefer to not download the images you may set download_images to false, but you either have to set "Secure connections" to "preferred" or have a custom certificate set (both options are found in your Plex server's network settings). This is needed because the default SSL certificate supplied by Plex is for their own domain and not for your Plex server. If your Plex server provides it's own certificate you only need to set ssl_cert to true and download_images to false.

**Do not just copy examples, please use config options above to build your own!**
### Sample for configuration.yaml:

    sensor:
    - platform: plex_recently_added
      token: YOUR_PLEX_TOKEN
      server_name: PLEX_SERVER_NAME
      ssl: true
      ssl_cert: false
      download_images: false
      max: 5

### Sample for ui-lovelace.yaml:

    - type: custom:upcoming-media-card
      entity: sensor.plex_recently_added


### Card Content Defaults

| key | default | example |
| --- | --- | --- |
| title | $title | "The Walking Dead" |
| line1 | $episode | "What Comes After" |
| line2 | $day, $date $time | "Monday, 10/31 10:00 PM" Displays time of download.|
| line3 | $number - $rating - $runtime | "S01E12 - ★ 9.8 - 01:30"
| line4 | $genres | "Action, Adventure, Comedy" |
| icon | mdi:eye-off | https://materialdesignicons.com/icon/eye-off

