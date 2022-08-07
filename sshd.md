# sshd: no hostkeys available -- exiting

> https://www.garron.me/en/linux/sshd-no-hostkeys-available-exiting.html

- Generate keys
`doas ssh-keygen -A`

- Start sshd with absolute path
`doas /usr/bin/sshd`

- Disable firewall if required (If using sshd permanently, add a rule)
`doas sv stop iptables`

