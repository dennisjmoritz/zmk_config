# ZMK Config for DJ-Sofle Keyboard

This repository contains ZMK configuration for a Sofle keyboard with support for both wireless split operation and dongle mode.

## Build Targets

- `sofle_left` - Left half of the keyboard (nice nano v2)
- `sofle_right` - Right half of the keyboard (nice nano v2) 
- `sofle_dongle` - USB dongle receiver (nice nano v2)
- `settings_reset` - Reset settings shield

## Dongle Mode

The `sofle_dongle` configuration creates a USB dongle that acts as a central receiver for both keyboard halves. This allows you to use the keyboard wirelessly while having a single USB connection to your computer.

### Setup Instructions

1. Flash the `sofle_dongle` firmware to a nice nano v2 board
2. Flash `sofle_left` firmware to the left keyboard half
3. Flash `sofle_right` firmware to the right keyboard half
4. Connect the dongle to your computer via USB
5. Pair both keyboard halves with the dongle

The dongle will appear as "DJ-Sofle-Dongle" and relay all keypresses from both halves over USB.