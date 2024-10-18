# check_uptimerobot_monitor
Monitor UptimeRobot for Nagios using the UptimeRobot API.

**Important:** A read-only API key is required. You can generate one by navigating to https://dashboard.uptimerobot.com > Integrations & API > API > Read-only API key > + Create.

## Usage
```
Usage: check_uptimerobot_monitor.sh -a <api-key> [-m <monitor>] [-v] [-V] [-h]
  -a  API Key (required)
  -m  Monitor ID (optional)
  -v  Verbose (optional)
  -V  Version (optional)
  -h  Help (optional)
```
## Installation
- Copy check_uptimerobot_monitor to [nagios_path]/libexec
- Set permissions to 0755 for check_uptimerobot_monitor
- Define custom commands for check_uptimerobot_monitor in commands.cfg
```
define command {
  command_name check_uptimerobot_monitor
  command_line $USER1$/check_uptimerobot_monitor -a $ARG1$ -m $ARG2$
}

define command {
  command_name check_uptimerobot_monitors
  command_line $USER1$/check_uptimerobot_monitor -a $ARG1$
}
```
- Define custom services for host
```
define service{
  use                 generic-service
  host_name           HOSTNAME
  service_description www.example.com
  check_command       check_uptimerobot_monitor!API_KEY!123456789
}

define service{
  use                 generic-service
  host_name           HOSTNAME
  service_description All sites
  check_command       check_uptimerobot_monitors!API_KEY
}
```
