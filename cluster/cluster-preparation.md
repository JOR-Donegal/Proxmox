# Cluster Preparation

For the things we need to prepare, I will use the command prompt, I will use SSH and Putty.

## Locale

Verify the locale of each server. I used the default **US.UTF-8**. If you used anything else, use

```
dpkg-reconfigure locales
```

to add the locale on each server.

## Connectivity

Previously we configured entries for each server in the hosts file. Do a ping test and make sure each server is visible to the others.

