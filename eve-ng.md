

If eve-ng gets stuck at web interface loading screen, this might be caused by a problematic lab:

```
ls /opt/unetlab/labs/
```

If there is something there move it to your user's home directory:

```
mv /opt/unetlab/labs/* ~
```

Test logging in in web interface, it should work.
