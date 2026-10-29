# Home Assistant blueprints

## Internet watchdog - power-cycle the modem plug

[![Import blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fmversion%2Fhome-assistant-blueprints%2Fblob%2Fmain%2Finternet-watchdog-plug.yaml)

When Home Assistant can't reach the internet for a set time (default 2 minutes), it turns off the
smart plug powering the modem/router, waits (default 15 seconds) and turns it back on. If the
internet isn't back within the recovery time (default 10 minutes) it tries again, up to a maximum
number of attempts (default 3), and always leaves the plug on at the end.

**Needs:**

- Home Assistant 2024.10 or later.
- One or more **Ping (ICMP)** binary sensors, for example 1.1.1.1 and 8.8.8.8. The plug is only
  cycled when all of them are offline.
- A smart plug exposed as a `switch`. It was built for an IKEA INSPELNING on Zigbee2MQTT.

**Two rules:**

- The plug must power the modem only, never the Home Assistant box.
- Set the plug's power-on behaviour to **Previous**, so it comes back on after a power cut.
  Avoid **On**: an IKEA INSPELNING set to On restarted itself as it switched off and came straight
  back on, so the modem never lost power. Avoid **Toggle** too, because a power cut would leave the
  modem off.

**Manual import:** Settings → Automations & scenes → Blueprints → Import blueprint, and paste:

```
https://github.com/mversion/home-assistant-blueprints/blob/main/internet-watchdog-plug.yaml
```
