# Secure Linux Server Permissions

## Goal
Restrict access to two shared folders using Linux users, groups and permissions.

## Setup
- Groups: developers, auditors
- Users: harsh (developers), ronak (auditors), carol (no group)
- /srv/devdata: owner root, group developers, mode 2770 (rwxrws---)
- /srv/reports: owner harsh, group auditors, mode 750 (rwxr-x---)

## Results
| Test | Result |
|------|--------|
| harsh writes to /srv/devdata | Allowed |
| ronak lists /srv/devdata | Permission denied |
| carol lists /srv/devdata | Permission denied |
| harsh writes to /srv/reports | Allowed (owner) |
| ronak reads /srv/reports | Allowed (auditors, read-only) |
| ronak writes to /srv/reports | Permission denied |
| carol reads /srv/reports | Permission denied |

## Notes
- The setgid bit (the "s" in 2770) makes new files inherit the developers group.
- Tests were run with `sudo -u <user>` to act as each user.
