---
layout: page
title: "Google Maps Location Sharing"
description: "Instructions how to use Google Maps Location Sharing to track devices in Home Assistant."
date: 2017-02-12 10:00
sidebar: true
comments: false
sharing: true
footer: true
logo: google_maps.png
ha_release: 0.67
ha_category: Presence Detection
ha_iot_class: "Cloud Polling"
---

The `google_maps` platform allows you to detect presence using the unofficial API of [Google Maps Location Sharing](https://myaccount.google.com/locationsharing). 

You first need to create an additional Google account and share your location with that account. This platform will use that account to fetch the location of your device(s). You have to setup sharing through the Google Maps app on your mobile phone. You can find more information [here](https://support.google.com/accounts?p=location_sharing).  2FA and Google App passwords don’t yet work with this service and the Google account used for tracking.

This platform will create a file named `.google_maps_location_sharing.cookies` where it caches your login session, once the service successfully authenticates to Google.

<p class='note warning'>
Since this platform is using an unofficial API with the help of [locationsharinglib](https://github.com/costastf/locationsharinglib), Google may block access to your data the first time you've logged in with this component.  This issue can be fixed by logging in with your new account and approving your login on the [Device Activity](https://myaccount.google.com/device-activity) page.
</p>

Once the service is working, the device will be created in the known_devices.yaml file. You can change the “name:” field, but not the first field starting with “google_maps_”. If you do, that will break the device tracking and it will be recreated as a new device again.

To integrate Google Maps Location Sharing in Home Assistant, add the following section to your `configuration.yaml` file:

```yaml
# Example configuration.yaml entry
device_tracker:
  platform: google_maps
  username: example@gmail.com
  password: password
```

{% configuration %}
username:
  description: The email address for the Google account that has access to your shared location.
  required: true
  type: string
password:
  description: The password for your given username.
  required: true
  type: string
{% endconfiguration %}
