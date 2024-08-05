# ansible-role-rtpproxy

Ansible role for installing RTPProxy

![CI](https://github.com/miarec/ansible-role-rtpproxy/actions/workflows/ci.yml/badge.svg?event=push)


# Role Variables

For a full list of variables, see [defaults/main.yml](./defaults/main.yml)

## Installation Variables

 - `rtpproxy_version`: version of RTPProxy to install, default = `latest`. Check the available releases at [RTPProxy github repo](https://github.com/sippy/rtpproxy/releases)
 - `rtpproxy_user`: linux user to run the service, default = `rtpproxy`
 - `rtpproxy_group`: linux group the linux user belongs to, default = `rtpproxy`

 - `rtpproxy_cleanup_downloads`: when true, source download files will be deleted after successful install, default = `true`
 - `rtpproxy_force_install`: when true, RTPPRoxy will be installed and configured, even if RTPProxy is already installed. default = `false`

## Network Settings

 - `rtpproxy_ctrl_socket`: The control socket for RTPPRoxy. 

## Logging

- `rtpproxy_log_dir`: directory for log files, default = `/var/log/rtpproxy`
- `rtpproxy_log_file`: name of path to redis log file, default = `rtpproxy.log`



# Known issues

RTPProxy release files for 3.x are broken. They do not include external, like libucl

During complication, we see the error:

    libucl_test.c:10:10: fatal error: ucl.h: No such file or directory

It looks, the developers didn't expect the application is compiled from GitHub source files rather than release files.


At the same time, the release files for 2.x version are referencing `<sys/sysctl.h>` file that has been removed in the latest glibc.
