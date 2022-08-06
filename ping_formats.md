
Ping in decimal, hex, octal or even binary by using `$(([BASE]#[VALUE]))` where `BASE` is the base you want to use like `2` for binary `16` hex and so on; and `VALUE` is the value in that base

```
ping 0xa.0x1.0xa.0x1
ping 0x0a.0x01.0x00a.0x1
ping 1010.1.1010.1
ping b1010.b1.b1010.b1
ping b'ls1010.b1.b1010.b1
ping b'1010'.b'1'.b'1010'.b'1'
ping $((2#1010)).$((2#1)).$((2#1010)).$((2#1))
ping $((2#1010)).$((2#0001)).$((2#1010)).$((2#0001))
ping $((16#a)).$((16#0001)).$((16#a)).$((16#0001))
ping $((2#a)).$((2#0001)).$((2#a)).$((2#0001))
ping $((16#a)).$((2#0001)).$((16#a)).$((2#0001))
ping 0xa.$((2#0001)).0xa.$((2#0001))
```
