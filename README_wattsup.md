# Zaptec WattsUp — Lovelace Card

A custom Home Assistant Lovelace card for the Zaptec WattsUp EV charger, integrated via Tibber.

## Features

- **Status badge** — Disconnected / Connected / Charging with colour-coded pill (green, amber, grey)
- **Live charge power** — Large display in W or kW
- **Energy metrics** — This session, Last session, Lifetime (each in a bordered box)
- **Connected car** — Shows the car currently plugged in (Sally or Bonnie) with name, SoC bar, target marker, and range
- **Charge current slider** — Mushroom number card to set available current (0–16A)
- **Charge Now button** — Single green button to start charging; only visible when a car is plugged in

## Requirements

- [custom:button-card](https://github.com/custom-cards/button-card) (HACS)
- [Mushroom Cards](https://github.com/piitaya/lovelace-mushroom) (HACS)
- Zaptec integration via Tibber
- Tibber integration for car presence detection

## Entities Used

| Entity | Purpose |
|---|---|
| `binary_sensor.wattsup_plug` | Cable connected |
| `binary_sensor.wattsup_charging` | Charging active |
| `sensor.wattsup_charge_power` | Live charge power (W) |
| `sensor.wattsup_session_total_charge` | This session energy (kWh) |
| `sensor.wattsup_completed_session_energy` | Last session energy (kWh) |
| `sensor.wattsup_energy_meter` | Lifetime energy (kWh) |
| `number.karrsbackevagen_4_available_current` | Available current (0–16A) |
| `switch.wattsup_charging` | Start charging |
| `binary_sensor.sally_plug` | Sally car presence detection |
| `sensor.sally_state_of_charge` | Sally SoC (%) |
| `sensor.sally_target_state_of_charge` | Sally charge target (%) |
| `sensor.sally_estimated_remaining_driving_range` | Sally range (km) |
| `sensor.tesla_3_p74d_state_of_charge` | Bonnie SoC (%) |
| `sensor.tesla_3_p74d_target_state_of_charge` | Bonnie charge target (%) |
| `sensor.tesla_3_p74d_estimated_remaining_driving_range` | Bonnie range (km) |

## Car Detection Logic

The card checks `binary_sensor.sally_plug`. If Sally's plug sensor is `on` at the same time as the WattsUp plug, Sally is the connected car — otherwise Bonnie is shown. Both plug sensors are provided by the Tibber integration and update simultaneously on connect.

## Installation

1. Copy `zaptec_wattsup_card.yaml` contents
2. In HA, go to your dashboard → Edit → Add Card → Manual
3. Paste the YAML and save
