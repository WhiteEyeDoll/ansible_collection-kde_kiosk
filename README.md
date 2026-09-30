# KDE kiosk

`whiteeyedoll.kde_kiosk` provisions a KDE Wayland touchscreen kiosk with an
optional Firefox app. Targets AlmaLinux 10 and RHEL 10; requires Ansible Core
2.16+, SSH/sudo access, and Wayland-capable graphics.

## Install locally

```sh
mkdir -p dist
ansible-galaxy collection build --output-path dist --force
ansible-galaxy collection install dist/whiteeyedoll-kde_kiosk-0.1.0.tar.gz --force
```

## Configure and run

```sh
mkdir -p inventory
cp examples/inventory.yml inventory/hosts.yml
```

Edit the host address, SSH user, and `firefox_kiosk_urls`, then run:

```sh
ansible-playbook whiteeyedoll.kde_kiosk.kiosk -i inventory/hosts.yml --ask-become-pass
```

Add `--ask-pass` for SSH password authentication. Use
`whiteeyedoll.kde_kiosk.base` for KDE without an app.

Configuration changes restart the graphical session. Set `kiosk_activate: false`
to defer activation until reboot or manual restart. Unchanged runs do not restart it.

See the role [defaults](roles/kiosk/defaults/main.yml) and
[Firefox defaults](roles/firefox/defaults/main.yml) for available settings.
