Github actions that are shared by multiple puara projects

## Available Actions

### generate-arduino-library

Generates the `puara-arduino` library from source templates and modules.

**What it does:**
- Checks out `puara-module` and `puara-module-templates` repositories
- Checks out the `puara-arduino` repository (requires token for write access)
- Copies module sources and compiles templates into Arduino example sketches
- Uploads the generated library as an artifact

**Inputs:**
- `puara-arduino-repo-token` (required): GitHub token for accessing the puara-arduino repository

### lint-arduino-library

Lints the Arduino library for compliance and quality standards.

**What it does:**
- Downloads the `puara-arduino` artifact from a previous workflow step
- Runs Arduino Lint with strict compliance and library manager submission checks

**Requires:**
- The `puara-arduino` artifact to be available (typically from `generate-arduino-library`)

### compile-arduino-library

Compiles the Arduino library against multiple microcontroller boards to ensure compatibility.

**What it does:**
- Downloads the `puara-arduino` artifact
- Installs Arduino CLI and required board cores (ESP32)
- Installs library dependencies (OSC, ArduinoBLE)
- Compiles example sketches for 4 different board types:
  - TinyPICO
  - XIAO ESP32-S3
  - M5StickC
  - ESP32-C3 Dev Module

**Examples compiled:**
- basic
- OSC-Duplex
- OSC-Send
- OSC-Receive
- ble-advertising

### push-arduino-library

Pushes the generated Arduino library to the `puara-arduino` repository.

**What it does:**
- Checks out the `puara-module` and `puara-arduino` repositories
- Downloads the updated `puara-arduino` artifact
- Commits and pushes changes to the `continuous` branch of `puara-arduino`
- Only commits if there are actual changes

**Inputs:**
- `puara-arduino-repo-token` (required): GitHub token for write access to puara-arduino

