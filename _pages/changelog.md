---
layout: single
paginate: false
entries_layout: list
author_profile: true
classes: wide
---

# SADMIN Tools Changelog

## Release v[1.3.2](https://github.com/jadupl2/sadmin/releases) (2021-04-30)

### Enhancements
- 2021_03_05 sadm_osupdate_starter.sh (v4.3) - Added sleep time after update to allow system to  become available.
- 2021_03_24 sadmlib_std.sh (v3.67) - Non root user MUST be part of 'sadmin' group to use SADMIN library.
- 2021_03_29 sadm_backup.sh (v3.28) - Exclude list is shown before each backup (tar) begin.
- 2021_03_29 sadm_backup.sh (v3.29) - Log of each backup (tar) recorded and place in backup directory.
- 2021_04_19 sadm_server_rear_backup.php (v1.4) - Change "Exclude" to "Include/Exclude" Label on file config
- 2021_04_19 sadm_setup.py (v3.54) - Fix Path to sadm_service_ctrl.sh

### Fixes
- 2021_04_01 sadm_daily_report.sh (v1.23) - Fix problem when the last line of *.rch was a blank line.
- 2021_04_02 sadmlib_std.sh (v3.68) - Replace test using '-v' with '! -z' on variable.
- 2021_04_09 sadmlib_std.sh (v3.69) - Fix problem with disabling log header, log footer and rch file.
- 2021_04_28 sadm_daily_report.sh (v1.24) - Fix problem with the report servers exclude list.


---
<br>
