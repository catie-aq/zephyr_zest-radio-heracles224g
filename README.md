# Zest_Radio_Heracles224G

Zest_Radio_Heracles224G board support for Zephyr OS.

## Usage

This board enables the following component:

- [SIMCom Heracles 224G](https://www.simcom.com/) GSM / LTE Cat-M1 / NB-IoT modem.

💡 This driver should also be added to your workspace:

- [SIMCom Heracles 224G driver](https://github.com/catie-aq/zephyr_simcom-heracles224g).

:pushpin: This shield defines:

- a cellular modem device: `heracles224g_zest_radio_heracles224g_<port>`.

:triangular_ruler: To use this shield:

- Update your device tree by adding the `ZEST_RADIO_HERACLES224G(port)` macro to the `app.overlay`
  file.\
  Replace `port` with the number of the Zest_Core port to which the shield is connected, e.g.:

  ```dts
  ZEST_RADIO_HERACLES224G(1) /* Zest_Radio_Heracles224G connected to Zest_Core first port */
  ```

- Enable the cellular modem and the network stack in `prj.conf`, e.g.:

  ```
  CONFIG_NETWORKING=y
  CONFIG_NET_L2_PPP=y
  CONFIG_NET_IPV4=y
  CONFIG_NET_SOCKETS=y
  CONFIG_MODEM=y
  CONFIG_MODEM_CELLULAR=y
  CONFIG_MODEM_CELLULAR_APN="your.apn"
  ```

- Activate support for the shield by adding `--shield zest_radio_heracles224g` to the west command.

## Advanced Usage

This shield can be hardware-modified to suit your application.
In that case, use instead the alternate variant of the shield:

- Update your device tree by adding the `ZEST_RADIO_HERACLES224G_ALT(port, pwrkey, status, dtr)`
  macro to the `app.overlay` file, with:
  - `port`: number of the Zest_Core port to which the shield is connected,
  - `pwrkey`: modem PWRKEY control pin (`DIO2` default, `DIO1` or `DIO4`),
  - `status`: modem STATUS pin (`DIO7` default),
  - `dtr`: modem DTR pin (`DIO10` default).

  ```dts
  ZEST_RADIO_HERACLES224G_ALT(1, DIO1, DIO7, DIO10) /* Zest_Radio_Heracles224G connected to Zest_Core first port */
  ```

- Activate support for the shield by adding `--shield zest_radio_heracles224g_alt` to the west
  command.

:warning: The alternate UART routing (DIO12 / DIO18) and the hardware flow control (ADC3 / ADC4)
are not supported by this shield description.
