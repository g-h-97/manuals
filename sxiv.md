

Edit `window.c` for background and foreground colors

```c
	bg = win_res(db, RES_CLASS ".background", "black");
	fg = win_res(db, RES_CLASS ".foreground", "white");
```

Edit `config.def.h` for thumb nail size, add more as you see fits

```c
/* thumbnail sizes in pixels (width == height): */
static const int thumb_sizes[] = { 32, 64, 96, 128, 160, 256 };

/* thumbnail size at startup, index into thumb_sizes[]: */
static const int THUMB_SIZE = 5;
```

# Void Linux build requirements

```
imlib2-devel
libexif-devel
giflib-devel
```
