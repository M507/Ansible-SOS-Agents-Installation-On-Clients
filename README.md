## SOS-Agents-Installation-On-Clients

This playbook configures rsyslog and installs Osquery Fleet launcher.

## Steps to use:
- Change sos_server variable in var.yml.
- Linux
    - Download DEB and RPM osquery packages from `https://sos_server/#/downloads`. You should have two files:
        - deb-launcher.deb
        - rpm-launcher.rpm
    - Copy the two downloaded files to `roles/nix_monitor/files/`
- Windows
    - Download all msi files from `https://sos_server/#/downloads`. You should have three files. Rename and standardize their names to:
        - msi-launcher.msi
        - wazuh-agent.msi
        - winlogbeat-oss.msi
    - Copy the three renamed files to `roles/win_monitor/files/`
    - Edit the `winlogbeat.yml` config file in `roles/win_monitor/files/`.
- Install the dependencies mentioned in `dependencies.sh`.
- Edit `hosts.ini` according to your network then enjoy : )


Expected output:
```sh
PLAY [all] *****************************************************************************************************************************************

TASK [Gathering Facts] *****************************************************************************************************************************
ok: [10.100.200.2]

TASK [monitor : Include fleet] *********************************************************************************************************************
included: /root/sos-clients/roles/monitor/tasks/fleet.yml for 10.100.200.2

TASK [monitor : Copy Fleet launcher package if debian/Ubuntu] **************************************************************************************
changed: [10.100.200.2]

TASK [monitor : Install Fleet launcher if debian/Ubuntu] *******************************************************************************************

changed: [10.100.200.2]

TASK [monitor : Copy Fleet launcher package on CentOS/Redhat] **************************************************************************************
skipping: [10.100.200.2]

TASK [monitor : Install Fleet launcher if CentOS/Redhat] *******************************************************************************************
skipping: [10.100.200.2]

TASK [monitor : Start Fleet launcher] **************************************************************************************************************
ok: [10.100.200.2]

TASK [monitor : Enable Fleet launcher] *************************************************************************************************************
ok: [10.100.200.2]

TASK [monitor : Include Rsyslog] *******************************************************************************************************************
included: /root/sos-clients/roles/monitor/tasks/rsyslog.yml for 10.100.200.2

TASK [monitor : Add a line to a rsyslog conf] ******************************************************************************************************
changed: [10.100.200.2]

TASK [monitor : Restart Rsyslog] *******************************************************************************************************************
changed: [10.100.200.2]

TASK [monitor : Enable Rsyslog] ********************************************************************************************************************
ok: [10.100.200.2]

TASK [monitor : Include wazuh] *********************************************************************************************************************
skipping: [10.100.200.2]

PLAY RECAP *****************************************************************************************************************************************
10.100.200.2            : ok=10   changed=4    unreachable=0    failed=0   


```

### Agents
- :heavy_check_mark: CentOS/Redhat and Debian/Ubuntu Fleet launcher + osquery
- :heavy_check_mark: CentOS/Redhat and Debian/Ubuntu Rsyslog
- :black_square_button: CentOS/Redhat and Debian/Ubuntu Wazuh
- :heavy_check_mark: Windows Fleet launcher + osquery
- :heavy_check_mark: Windows Wazuh
- :heavy_check_mark: Windows Winlogbeat

