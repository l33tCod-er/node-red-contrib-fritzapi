# node-red-contrib-fritzapi

Control your smart home DECT devices and guest wifi through an AVM Fritz!Box with node-RED.

These nodes are a simple Node-RED wrapper for [andig's](https://github.com/andig) ever-popular
[fritzapi](https://www.npmjs.com/package/fritzapi), see there a for feature description.

## Installation

The recommended way is to install directly from Node-RED under `Manage palette`.

Manual installation:

```bash
cd ~/.node-red
npm install node-red-contrib-fritzapi
```

## Configuration

Depending on your FRITZ!Box configuration, a user name may be needed. If your box is configured for password-only
admin access, leave the user name blank and only provide the admin password. Make sure that smart home control is
enabled on the FRITZ!Box.

## Usage

The packages contains `thermostat`, `switch` and `guest wifi` nodes under the `advanced` section in the palette.
Thermostats and switches expect an actuator identification number `AIN` as `ain` or `topic` on the input message.
If both `ain` and `topic` are provided, `ain` has precedence.
Nodes have an (optional) pre-set action. It can be overriden with the `action` attribute on input messages. 
See [fritzapi](https://www.npmjs.com/package/fritzapi) for a list of supported action names.

Any payload is accepted for information retrieval. For switch and wifi updates, send the desired boolean value
(on or off). For thermostat updates, send the target temperature or adjustment in degrees Celsius.
Temperature and outlet adjustments are only made if the desired state differs from the actual state.
All updates are logged.

There are two special cases: `setTempComfort` (Set to day temperature) and `setTempNight` (Set to night temperature)
do not expect a temperature as payload, because they set the *target* temperature to the day / night preset.

All actions output the requested or updated value.

**There is a comprehensive example flow which demonstrates all use cases of the `thermostat` node.**

## To Do

- Switches are not tested, as I do not own any. All feedback appreciated.
- Guest Wifi control does not seem to work with FRITZ!OS 7.x

## Credits

- Kudos to [andig](https://github.com/andig) for [fritzapi](https://www.npmjs.com/package/fritzapi).
- Also, substantial parts of the low-level interface were also written by [andig](https://github.com/andig) for
[homebridge-fritz](https://www.npmjs.com/package/homebridge-fritz). Thanks for the wizardry!

## License

[MIT](https://opensource.org/licenses/MIT)
