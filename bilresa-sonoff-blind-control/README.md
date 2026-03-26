# BILRESA + Sonoff Dual Switch – Electric Blind Control

Control a pair of electric blinds using the IKEA BILRESA E2489 Matter dual-button remote and two Sonoff switches.

## Requirements

- IKEA BILRESA E2489 Matter dual-button remote
- Two Sonoff switches wired to your electric blinds
- An `input_number` helper entity (15-30 seconds range, 15-second increments) for adjustable duration
- Home Assistant 2025.12.1 or later

## Button Mapping

| Button | Action | Result |
|--------|--------|--------|
| Button 1 | Single press | If running → stop both switches; if idle → increase duration +15s |
| Button 1 | Double press | Switch 1 ON for `duration_helper` value, then OFF |
| Button 1 | Long press | Switch 1 ON while held, OFF on release |
| Button 2 | Single press | If running → stop both switches; if idle → decrease duration -15s |
| Button 2 | Double press | Switch 2 ON for `duration_helper` value, then OFF |
| Button 2 | Long press | Switch 2 ON while held, OFF on release |

## Configuration

| Input | Description | Default |
|-------|-------------|---------|
| Button 1 Event Entity | Event entity for BILRESA button 1 (e.g. `event.bilresa_button_1`) | — |
| Button 2 Event Entity | Event entity for BILRESA button 2 (e.g. `event.bilresa_button_2`) | — |
| Sonoff Switch 1 | Switch driven by Button 1 actions | — |
| Sonoff Switch 2 | Switch driven by Button 2 actions | — |
| Duration Helper | input_number entity storing run duration (15-30s, 15s steps) | — |
| Long Press Safety Timeout | Maximum seconds the switch can stay ON during a long press before auto-off | 40 |

## Notes

- **Single press behavior** — if a switch is running (ON), single press stops both switches. If idle, Button 1 increases the duration helper by 15s and Button 2 decreases it by 15s.
- **Long press safety timeout** — if the release event is not received (e.g. lost packet), the switch turns OFF automatically after this timeout to prevent the blind from running indefinitely.
- **`mode: restart`** — a new press correctly cancels any in-progress timed sequence (e.g. interrupting a double-press run with a single-press stop).
