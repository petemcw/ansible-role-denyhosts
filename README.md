# Denyhosts Role for Ansible

This role installs [DenyHosts](http://denyhosts.sourceforge.net/) is a python program that automatically blocks SSH attacks by adding entries to `/etc/hosts.deny`.

## Requirements

This role requires [Ansible](http://www.ansibleworks.com/) version 1.4 or higher and the Debian/Ubuntu platform.

## Role Variables

The variables that can be passed to this role and a brief description about
them are as follows:

```yaml
# The list of white-listed hosts that are added to `/etc/hosts.allow`
denyhosts_always_allow: []

# The default path for the log file containing SSHD logging info
denyhosts_secure_log: '/var/log/auth.log'

# The default path for the file that contains restricted hosts
denyhosts_hosts_deny: '/etc/hosts.deny'

# The duration in which denied older entries are removed when purge is run
denyhosts_purge_deny: ''

# The maximum number of times a host will be purged
denyhosts_purge_threshold: 0

# The service that will be blocked
denyhosts_block_service: 'sshd'

# The number of invalid user failed login attempts allowed before block
denyhosts_deny_threshold_invalid: 5

# The number of valid user failed login attempts allowed before block
denyhosts_deny_threshold_valid: 10

# The number of root user failed login attempts allowed before block
denyhosts_deny_threshold_root: 1

# The number of restricted user failed login attempts allowed before block
denyhosts_deny_threshold_restricted: 1

# The default path for DenyHosts to write data
denyhosts_work_dir: '/var/lib/denyhosts'

# The default flag on whether to report suspicious activity from allowed hosts
denyhosts_suspicious_login_report_allowed_hosts: 'YES'

# The default flag on whether to lookup the hostname for reported IPs
denyhosts_hostname_lookup: 'YES'

# The default path for DenyHosts running lock file
denyhosts_lock_file: '/run/denyhosts.pid'

# The default recipient of reports
denyhosts_admin_email: 'root@localhost'

# The email server host used to send reports
denyhosts_smtp_host: 'localhost'

# The email server port used to send reports
denyhosts_smtp_port: 25

# The default sender of reports
denyhosts_smtp_from: 'DenyHosts <nobody@localhost>'

# The default report subject
denyhosts_smtp_subject: 'DenyHosts Report'

# The default date format for reports
denyhosts_smtp_date_format: '%a, %d %b %Y %H:%M:%S %z'

# The default flag of whether to send data to syslog
denyhosts_syslog_report: 'NO'

# The default flag of whether to lookup hostnames for allowed IPs
denyhosts_allowed_hosts_hostname_lookup: 'NO'

# The duration between failed valid login attempts that trigger a failed count reset
denyhosts_age_reset_valid: '5d'

# The duration between failed root login attempts that trigger a failed count reset
denyhosts_age_reset_root: '25d'

# The duration between failed restricted login attempts that trigger a failed count reset
denyhosts_age_reset_restricted: '25d'

# The duration between failed invalid login attempts that trigger a failed count reset
denyhosts_age_reset_invalid: '10d'

# The default flag to reset failed count when login successful
denyhosts_reset_on_success: 'YES'

# The default program to be run when host is denied
denyhosts_plugin_deny: false

# The default program to be run when host is purged
denyhosts_plugin_purge: false

# The regular expression used to identify additional hackers for your SSH config
denyhosts_userdef_failed_entry_regex: false

# The default path for DenyHosts logfile
denyhosts_daemon_log: '/var/log/denyhosts'

# The default DenyHosts log timestamp format
denyhosts_daemon_log_time_format: false

# The default DenyHosts log message format
denyhosts_daemon_log_message_format: '%(asctime)s - %(name)-12s: %(levelname)-8s %(message)s'

# The default duration DenyHosts will pause between polling
denyhosts_daemon_sleep: '30s'

# The default duration DenyHosts will pause between purge runs
denyhosts_daemon_purge: '1h'

# The default flag for whether to enable synchronization features
denyhosts_enable_sync: false

# The default duration between synchronizations
denyhosts_sync_interval: '1h'

# The default flag for whether to upload denied host data
denyhosts_sync_upload: 'YES'

# The default flag for whether to download denied host data
denyhosts_sync_download: 'YES'

# The number of times downloaded hosts must have been denied before being added locally
denyhosts_sync_download_threshold: 3

# The default resiliency period
denyhosts_sync_download_resiliency: '5h'
```

## Examples

1. Install DenyHosts with default settings

    ```yaml
    ---
    # This playbook installs DenyHosts
    
    - name: Apply DenyHosts to all nodes
      hosts: all
      roles:
        - denyhosts
    ```

2. Install DenyHosts and enable synchronization

    ```yaml
    ---
    # This playbook installs DenyHosts
    
    - name: Apply DenyHosts to all nodes
      hosts: all
      roles:
        { role: denyhosts,
            denyhosts_enable_sync: true
        }
    ```

## Dependencies

None.

## License

MIT.
