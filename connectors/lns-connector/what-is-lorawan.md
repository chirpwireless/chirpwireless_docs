# What is LoRaWAN?

LoRaWAN (Long Range Wide Area Network) is the wireless technology that connects your sensors to Chirp. It's designed specifically for the kind of devices you find in a smart home — small sensors that send readings like temperature, humidity, or door status — and it does so over long distances while using almost no battery power.

Think of LoRaWAN as a wireless network built for sensors, not for streaming video or browsing the web. It sends tiny amounts of data very efficiently, which is exactly what a temperature sensor or a leak detector needs.

## Why LoRaWAN Works Well for Smart Homes

### Reaches Every Corner of Your Property

LoRaWAN uses sub-gigahertz radio frequencies that penetrate walls, floors, and concrete far better than Wi-Fi or Bluetooth. A sensor in the basement behind thick concrete walls, in the attic above insulation, or buried in a utility closet can still reach your gateway reliably. This is what makes LoRaWAN uniquely practical for homes — it reaches the places where Wi-Fi drops out.

A single gateway covers your entire property and often well beyond. In open areas the signal can travel several kilometers, so a shed at the back of the garden, a detached garage, or a greenhouse across the yard are all within easy reach. You don't need electricity or Wi-Fi in those spaces — just place a battery-powered LoRaWAN sensor and it connects on its own. Most home sensors are peel-and-stick — no wiring, no installation tools.

For the best coverage, place your gateway near a window or on the roof if possible. A window-mounted or roof-mounted gateway has a clear line to the surrounding property, giving you the largest radius of reliable reception around your home.

### Years of Battery Life

LoRaWAN sensors are designed to run for years on a single battery. A temperature sensor in your garden or a leak detector under the sink can operate for two to five years without attention. You don't need to wire them into mains power or change batteries every few months. This is why LoRaWAN is perfect for places with no power outlet — the sensor is the only thing you need.

### Secure Communication

All data between your sensors and Chirp is encrypted end-to-end. Your sensor readings, door status alerts, and environmental data travel securely — nobody can intercept or tamper with the data in transit.

### Works with Many Sensors at Once

A single gateway can handle hundreds of sensors simultaneously. Whether you have five sensors or fifty, one gateway is typically enough for a home setup.

## What Kinds of Sensors Use LoRaWAN?

LoRaWAN is ideal for sensors that send small readings at regular intervals:

- **Temperature and humidity** sensors for rooms, greenhouses, wine cellars
- **Door and window** open/close sensors for security
- **Water leak** detectors for bathrooms, basements, kitchens
- **Soil moisture** sensors for gardens and plant beds
- **Air quality** monitors for living spaces
- **Motion detectors** for entry points or driveways
- **Energy and utility** meters for tracking consumption

## How It Connects to Chirp

Your LoRaWAN sensors communicate with a **gateway** (a small device plugged into your home network). The gateway relays sensor data to Chirp's built-in network server, which processes it and makes it available in your dashboards, automations, and alerts. You don't need to set up or maintain any network infrastructure beyond the gateway itself.

For which frequency band your country uses, see [LoRaWAN Frequencies](lorawan-frequencies.md). For how Chirp handles the network automatically, see [Built-in Network Server](built-in-lns.md).
