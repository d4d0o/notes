#### Buildroot External Package local incremental rebuild

To catch local modification (not git push to remote) and rebuild based on that instead of behing overwritten by remote sources automatically pulled:

```
make AESD_ASSIGNMENTS_OVERRIDE_SRCDIR=~/aesd/assignments-3-and-later-d4d0o aesd-assignments-rebuild
```

or

```
make AESD_ASSIGNMENTS_OVERRIDE_SRCDIR=~/aesd/assignments-3-and-later-d4d0o aesd-assignments-rebuild all
```

To start from an empty build output

```
<packagename>-dirclean
```