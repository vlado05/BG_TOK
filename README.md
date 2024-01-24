[![](https://img.shields.io/github/release/vlado05/bg_electricity_regulated_pricing_bg_tok/all.svg?style=for-the-badge)](https://github.com/vlado05/bg_electricity_regulated_pricing_bg_tok/releases)
[![hacs_badge](https://img.shields.io/badge/HACS-Custom-orange.svg?style=for-the-badge)](https://github.com/hacs/integration)
[![](https://img.shields.io/github/license/vlado05/bg_electricity_regulated_pricing_bg_tok?style=for-the-badge)](LICENSE.txt)
[![](https://img.shields.io/github/workflow/status/vlado05/bg_electricity_regulated_pricing_bg_tok/Python%20package?style=for-the-badge)](https://github.com/vlado05/bg_electricity_regulated_pricing_bg_tok/actions)

# Цени на регулирания пазар на електроенергия в България за Home Assistant
Custom integration for [Home Assistant](https://www.home-assistant.io) that provides the price of electricity on the regulated market for domestic customers, and the applicable tariff, (day or night).

All three major regional providers, Electrohold, EVN, and ENERGO-PRO are supported.

The prices are defined statically as they change only about once a year. The official source for the current prices is section 6 from [Resolution C-14/30.06.2023 of the Bulgarian Energy and Water Regulatory Commission](https://www.dker.bg/uploads/reshenia/2023/res_c_14_23.pdf). All prices are the final amount that you'd pay, including VAT.

The night tariff starts at 22:00 UTC+2 and ends at 06:00 UTC+2. Note that even though Bulgaria switches to UTC+3 in the summer, meter clocks are not adjusted. In other words, the night tariff starts at 22:00/ends at 06:00 in the winter and at 23:00/07:00 in the summer.

> [!NOTE]
> Summary in Bulgarian: Интеграция за Home Assistant, която предоставя сензори за текущата цена на електроенергията и текущата тарифа (дневна или нощна) според часа и конфигурирания доставчик на електронергия. Предоставените цени са определени от КЕВР за трите основни доставчика на регулирания пазар: Електрохолд, EVN и ЕНЕРГО-ПРО. 

## Provided sensors

The integration provides two sensors that adjust according to the time of day and the configuration:

### Current price in BGN per kWh

This sensor provides the current price according to the configured provider and current tariff (day or night). It can be used to track expenses together with an energy meter in Home Assistant. The ID of the sensor will be `sensor.xxx_price` where `xxx` is derived from the name you give to the integration instance when configuring it. 
             
<img src="https://github.com/vlado05/bg_electricity_regulated_pricing_bg_tok/raw/main/images/price.png" width="50%" height="auto">

### Current tariff (day or night)

This sensor provides the current tariff. It can be used to run power-hungry devices when the night tariff starts. The ID of the sensor will be `sensor.xxx_tariff` where `xxx` is derived from the name you give to the integration instance when configuring it.

<img src="https://github.com/vlado05/bg_electricity_regulated_pricing_bg_tok/raw/main/images/tariff.png" width="50%" height="auto">

## Install

You can install the integration as a [custom HACS repository](https://hacs.xyz/docs/faq/custom_repositories/) using the GitHub URL of this project: https://github.com/avataar/bg_electricity_regulated_pricing. 

You can also install the integration by copying the [custom_components/bg_electricity_regulated_pricing](custom_components/bg_electricity_regulated_pricing) folder to your Home Assistant's `custom_components` folder just like with any other manually installed custom integration.

In the future, the integration may be added to HACS's default repositories.

## Configuration

From the sidebar in Home Assistant, select [Settings > Devices & Services](https://my.home-assistant.io/redirect/integrations). Search for the integration by name (Bulgarian Electricity Regulated Pricing / Цени на електроенергията на регулирания пазар в България). To configure it for most users, it will suffice to enter a name, choose the provider, and leave the rest of the options with their default values. The name will be used to derive the sensor IDs.

<p>
  <img src="https://github.com/vlado05/bg_electricity_regulated_pricing_bg_tok/raw/main/images/configure-bg.png" width="45%" height="auto">
  <img src="https://github.com/vlado05/bg_electricity_regulated_pricing_bg_tok/raw/main/images/configure-en.png" width="45%" height="auto">
</p>

If you have multiple meters to track, you can configure as many instances of the integration as needed.

### Advanced options

#### Custom provider

If the price you pay for your electricity is different from the three regional providers (but you still have a dual/single tariff like anyone else) you can configure custom prices. Choose `Custom` / `Потребителска цена` for the provider and enter the day/night price in the corresponding options below.

#### Incorrect meter clock

Meter clocks are notoriously never correct. You can adjust the time used for switching to the day/night tariff using the `Clock offset` / `Избързване/изоставане на часовника` option. This is the offset of the meter clock from real time. For example, if your meter clock is 30 minutes ahead set it to 30; if it's 15 minutes behind set it to -15.

#### Dual vs single tariff billing

Most users get billed at the dual tariff that switches between day and night prices. If for some reason you have a single tariff you can choose that in the `Tariff Type` / `Тарифност` option. When a single tariff is configured, the day price will be used at all times and the tariff sensor will always report the tariff as `day`.
