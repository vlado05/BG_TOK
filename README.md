[![](https://img.shields.io/github/release/vlado05/bg_electricity_regulated_pricing_bg_tok/all.svg?style=for-the-badge)](https://github.com/vlado05/bg_electricity_regulated_pricing_bg_tok/releases)
[![hacs_badge](https://img.shields.io/badge/HACS-Custom-orange.svg?style=for-the-badge)](https://github.com/hacs/integration)
[![](https://img.shields.io/github/license/vlado05/bg_electricity_regulated_pricing_bg_tok?style=for-the-badge)](LICENSE.txt)
[![](https://img.shields.io/github/workflow/status/vlado05/bg_electricity_regulated_pricing_bg_tok/Python%20package?style=for-the-badge)](https://github.com/vlado05/bg_electricity_regulated_pricing_bg_tok/actions)

# БГ електроенергия - цена/тарифа
Персонализирана интеграция за Home Assistant, която осигурява цената на електрическата енергия на регулирания пазар за битови клиенти, както и приложимата тарифа (дневна/нощна).

Цените се определят статично, тъй като се променят само веднъж годишно. Официалният източник за текущите цени е раздел 6 от [РЕШЕНИЕ № Ц-17 от 30.06.2024 г.
КОМИСИЯТА ЗА ЕНЕРГИЙНО И ВОДНО РЕГУЛИРАНЕ](https://www.dker.bg/uploads/reshenia/2024/res-c-17-2024.pdf). Всички цени са крайната сума, която ще платите, с включен ДДС.

Нощната тарифа започва в 22:00 UTC+2 и приключва в 06:00 UTC+2. Имайте предвид, че въпреки че България преминава към UTC+3 през лятото, часовниците на измервателните уреди не се коригират. С други думи, нощната тарифа започва в 22:00 ч./приключва в 06:00 ч. през зимата и в 23:00 ч./07:00 ч. през лятото.

## Предоставени сензори

Интеграцията осигурява два сензора, които се настройват в зависимост от времето на деня и конфигурацията:

### Текуща цена в лева за kWh

Този сензор предоставя текущата цена в зависимост от конфигурирания доставчик и текущата тарифа (дневна или нощна). Той може да се използва за проследяване на разходите заедно с електромера в Home Assistant. Идентификаторът на сензора ще бъде `sensor.xxx_price`, където `xxx` се получава от името, което давате на интеграционната инстанция при конфигурирането ѝ.

### Текуща тарифа (дневна или нощна)

Този сензор предоставя текущата тарифа. Той може да се използва за стартиране на устройства, изискващи много енергия, когато започне да действа нощната тарифа. Идентификаторът на сензора ще бъде `sensor.xxx_tariff`, където `xxx` се получава от името, което давате на интеграционната инстанция при конфигурирането ѝ.

> [!NOTE]
> Интеграция за Home Assistant, която предоставя сензори за текущата цена на електроенергията и текущата тарифа (дневна или нощна) според часа и конфигурирания доставчик на електронергия. Предоставените цени са определени от КЕВР за трите основни доставчика на регулирания пазар: Електрохолд, EVN и ЕНЕРГО-ПРО.
> 
Това е fork за лични тестове. Препоръчвам да използвате оригинала на @avataar: https://github.com/avataar/bg_electricity_regulated_pricing
