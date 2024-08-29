---
title: LXC export ssh keys
---

To upload ssh keys to the container or VM

```
cat <public_key_file_on_host> | lxc exec <container> -- sh -c "cat >> /home/ubuntu/.ssh/authorized_keys"
```
If needed

### Restart ssh on remote

```
lxc exec VMName -- systemctl restart ssh
```