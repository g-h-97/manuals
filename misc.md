# "/etc/profile.d/perlbin.sh:6 command not found: append_path" for arch users

> https://n.ethz.ch/~dbernhard/etcprofiledperlbinsh6-command-not-found-append_path.html#:~:text=%2Fetc%2Fprofile.-,d%2Fperlbin.,found%3A%20append_path%22%20for%20arch%20users&text=It's%20probably%20because%20a%20config,%2Fprofile%20%2Fetc%2Fprofile.

In case you get something like this printed when starting zsh (or bash, csh, fish, etc. ):

```
/etc/profile.d/perlbin.sh:6: command not found: append_path
/etc/profile.d/perlbin.sh:8: command not found: append_path
/etc/profile.d/perlbin.sh:10: command not found: append_path   
```

It's probably because a config got updated but you have previously made changes to /etc/profile and is thus lagging behind some changes.

If you've made some changes to the file /etc/profile you can view the diff of diff /etc/profile /etc/profile.pacnew and update accordingly.

Or if you've not changed the file (or do not care), simply do:

```
sudo mv /etc/profile /etc/profile.old
sudo mv /etc/profile.pacnew /etc/profile
```
