# zbx-apcupsd
Zabbix Template for USB attached APC UPS

This template is pretty simple, it uses apcupsd to query the UPS over USB, and ingests that data into Zabbix.

Data collected:
- Battery Charge (%)
- Battery Voltage (V)
- Hi-Voltage Transfer Threshold (V)
- Lo-Voltage Transfer Threshold (V)
- Line Voltage (V)
- Minimum Battery Charge (Shutoff threshold) (%)
- Minimum Time on Battery Remaining (m)
- UPS State (status)
- Time Left on Battery (m)
- Current Load (W) (this value is imprecise, as it is calculated based off of the Load % and the nominal power rating (pulled from apcaccess and used as a macro))

Triggers:
- Power interruption - Operating on battery
- UPS Recharging - Battery is charging
- Time Remaining Low - Macro specified threshold for alerting on a low battery
- Time Remaining Very Low - Macro specified threshold for alerting on a critically low battery

User Macros:
- {$APC_NOM_WATTS} - Nominal watts pulled from apcaccess, user filled in, defaults to 650
- {$APC_REM_WARN} - Time remaining on battery warning value, defaults to 10 minutes
- {$APC_REM_CRIT} - Time remaining on battery critical value, defaults to 3 minutes

Instructions:
1. Install `apcupsd` using your package manager.
2. Verify that the UPS is accessible by running `apcaccess` and make sure that you see the values you expect.
3. Copy the userparameter file to your `/etc/zabbix_agent{d,2}.d/` directory, or wherever your Zabbix Agent user parameter files live.
4. Restart your Zabbix Agent.
5. Import the template XML
6. Assign the template to your host.
7. Make sure macros are at values that work for you.
