# Sugon S65-G20 能耗监控

## ipmitool

例子：
```
> ipmitool sdr | grep PSU1_POUT
PSU1_POUT        | 132 Watts         | ok

> ipmitool sdr | grep PSU1_POUT | awk '{print $3}'
132
```

### 命令选项
```
Commands:
	raw           Send a RAW IPMI request and print response
	i2c           Send an I2C Master Write-Read command and print response
	spd           Print SPD info from remote I2C device
	lan           Configure LAN Channels
	chassis       Get chassis status and set power state 底盘
	power         Shortcut to chassis power commands
	event         Send pre-defined events to MC
	mc            Management Controller status and global enables
	sdr           Print Sensor Data Repository entries and readings
	sensor        Print detailed sensor information
	fru           Print built-in FRU and scan SDR for FRU locators
	gendev        Read/Write Device associated with Generic Device locators sdr
	sel           Print System Event Log (SEL)
	pef           Configure Platform Event Filtering (PEF)
	sol           Configure and connect IPMIv2.0 Serial-over-LAN
	tsol          Configure and connect with Tyan IPMIv1.5 Serial-over-LAN
	isol          Configure IPMIv1.5 Serial-over-LAN
	user          Configure Management Controller users
	channel       Configure Management Controller channels
	session       Print session information
	dcmi          Data Center Management Interface
	sunoem        OEM Commands for Sun servers
	kontronoem    OEM Commands for Kontron devices
	picmg         Run a PICMG/ATCA extended cmd
	fwum          Update IPMC using Kontron OEM Firmware Update Manager
	firewall      Configure Firmware Firewall
	delloem       OEM Commands for Dell systems
	shell         Launch interactive IPMI shell
	exec          Run list of commands from file
	set           Set runtime variable for shell and exec
	hpm           Update HPM components using PICMG HPM.1 file
	ekanalyzer    run FRU-Ekeying analyzer using FRU files
	ime           Update Intel Manageability Engine Firmware
```
## 传感器
### Voltage Sensors
| Sensor Name   | Status | Current Reading |
| ------------- | ------ | --------------- |
| +VCORE0       | Normal | 1.773 Volts     |
| +VCORE1       | Normal | 1.764 Volts     |
| +VDDQ_AB_CPU0 | Normal | 1.205 Volts     |
| +VDDQ_CD_CPU0 | Normal | 1.205 Volts     |
| +VDDQ_EF_CPU1 | Normal | 1.205 Volts     |
| +VDDQ_GH_CPU1 | Normal | 1.195 Volts     |
| +1.05V_PCH    | Normal | 1.028 Volts     |
| +1.5V_PCH     | Normal | 1.469 Volts     |
| +12V          | Normal | 11.968 Volts    |
| +5V           | Normal | 4.887 Volts     |
| +3.3V         | Normal | 3.287 Volts     |
| +VBAT         | Normal | 3.3 Volts       |
| PSU1_VIN      | Normal | 225 Volts       |
| PSU1_VOUT     | Normal | 12.2 Volts      |
| PSU2_VIN      | Normal | 226 Volts       |
| PSU2_VOUT     | Normal | 12.2 Volts      |

### Current Sensors
| Sensor Name | Status | Current Reading |
| ----------- | ------ | --------------- |
| PSU1_IIN    | Normal | 0.8 Amps        |
| PSU1_IOUT   | Normal | 11 Amps         |
| PSU2_IIN    | Normal | 0.5 Amps        |
| PSU2_IOUT   | Normal | 5 Amps          |

### Power Supply
| Sensor Name | Status            | Current Reading |
| ----------- | ----------------- | --------------- |
| PSU1_PIN    | Normal            | 96 Watts        |
| PSU1_POUT   | Normal            | 132 Watts       |
| PSU1_State  | Presence Detected | 0x8001          |
| PSU2_PIN    | Normal            | 48 Watts        |
| PSU2_POUT   | Normal            | 60 Watts        |
| PSU2_State  | Presence Detected | 0x8001          |