

# Troubleshooting

If you're facing the following issue when running `from scapy.all import *`

```
Python 3.9.2 (default, Feb 20 2021, 18:40:11)
[GCC 10.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from scapy.all import *
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
  File "/home/hicham/.local/lib/python3.9/site-packages/scapy/all.py", line 16, in <module>
    from scapy.arch import *
  File "/home/hicham/.local/lib/python3.9/site-packages/scapy/arch/__init__.py", line 27, in <module>
    from scapy.arch.bpf.core import get_if_raw_addr
  File "/home/hicham/.local/lib/python3.9/site-packages/scapy/arch/bpf/core.py", line 30, in <module>
    LIBC = cdll.LoadLibrary(find_library("libc"))
  File "/usr/lib/python3.9/ctypes/util.py", line 330, in find_library
    _get_soname(_findLib_gcc(name)) or _get_soname(_findLib_ld(name))
  File "/usr/lib/python3.9/ctypes/util.py", line 147, in _findLib_gcc
    if not _is_elf(file):
  File "/usr/lib/python3.9/ctypes/util.py", line 99, in _is_elf
    with open(filename, 'br') as thefile:
FileNotFoundError: [Errno 2] No such file or directory: b'liblibc.a'
>>>
```

Edit the file `~/.local/lib/python3.9/site-packages/scapy/arch/bpf/core.py`

```
# ctypes definitions

- LIBC = cdll.LoadLibrary(find_library("libc"))
+ LIBC = cdll.LoadLibrary(find_library("c"))
LIBC.ioctl.argtypes = [c_int, c_ulong, c_char_p]
LIBC.ioctl.restype = c_int
```
