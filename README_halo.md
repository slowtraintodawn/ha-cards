# ChargeAmps Halo — Lovelace Card

A custom Home Assistant Lovelace card for the ChargeAmps Halo EV charger (Connector 1 / Type 2 socket), integrated via the ChargeAmps integration and Tibber.

## Features

- **Status badge** — Disconnected / Connected / Charging with colour-coded pill (green, amber, grey)
- **Live charge power** — Large display in W or kW
- **Energy metrics** — This session (N/A — see note), Last session (N/A — see note), Lifetime kWh
- **Connected car** — Shows the car currently plugged in (Bonnie or Sally) with name, SoC bar, target marker, and range
- **Charge current slider** — Mushroom number card to set max current on Connector 1 (0–16A)
- **Charge Now button** — Single green button to enable Connector 1; only visible when a car is plugged in

## Requirements

- [custom:button-card](https://github.com/custom-cards/button-card) (HACS)
- [Mushroom Cards](https://github.com/piitaya/lovelace-mushroom) (HACS)
- ChargeAmps integration
- Tibber integration for car presence detection

## Entities Used

| Entity | Purpose |
|---|---|
| `binary_sensor.chargey_connector_1_cable_connected` | Cable connected on Connector 1 |
| `binary_sensor.chargey_charging` | Charging active |
| `sensor.chargey_2106038265m_1_power` | Live charge power (W) |
| `sensor.chargey_2106038265m_total_energy` | Lifetime energy (kWh) |
| `number.chargey_connector_1_max_current` | Max current Connector 1 (0–16A) |
| `switch.chargey_connector_1` | Enable/disable Connector 1 |
| `binary_sensor.bonnie_plug` | Bonnie car presence detection |
| `sensor.tesla_3_p74d_state_of_charge` | Bonnie SoC (%) |
| `sensor.tesla_3_p74d_target_state_of_charge` | Bonnie charge target (%) |
| `sensor.tesla_3_p74d_estimated_remaining_driving_range` | Bonnie range (km) |
| `sensor.sally_state_of_charge` | Sally SoC (%) |
| `sensor.sally_target_state_of_charge` | Sally charge target (%) |
| `sensor.sally_estimated_remaining_driving_range` | Sally range (km) |

## Car Detection Logic

The card checks `binary_sensor.bonnie_plug`. If Bonnie's plug sensor is `on` at the same time as Connector 1 is connected, Bonnie is the connected car — otherwise Sally is shown. Both plug sensors are provided by the Tibber integration.

## Session Energy (N/A)

The ChargeAmps integration does not provide per-session energy. To enable "This session" tracking, a HA `integration` platform sensor and `utility_meter` helper are required, with an automation to reset on cable connect. This is a planned improvement.

## Connector 2

Connector 2 is a 240V outlet and is not used for EV charging. It is excluded from this card.

## Installation

1. Copy `chargeamps_halo_card.yaml` contents
2. In HA, go to your dashboard → Edit → Add Card → Manual
3. Paste the YAML and save
