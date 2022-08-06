Sources :
> https://wiki.archlinux.org/index.php/Uniform_look_for_Qt_and_GTK_applications

# GTK

## Scaling
In order to scale & select a GTK theme for applications use the following environment variables in you .zshenv file

```bash
# To .zshenv
export GDK_SCALE=2
export GDK_DPI_SCALE=-1 # putting this to 0.5 screwed up virmanager
```

You can also use `gsettings` like so. However this might not be perfect so change them as required

```bash
gsettings set org.gnome.desktop.interface text-scaling-factor 2
gsettings set org.gnome.desktop.interface scaling-factor 2
```


## Theming

Put your themes in `~/.themes` & in `/usr/share/themes`. And put you icon themes in `~/.icons` & `/usr/share/icons`, Then set the following

> NOTE : Download flat-remix themes from
> https://drasite.com/flat-remix
> Or
> https://github.com/daniruiz/Flat-Remix

```bash
gsettings set org.gnome.desktop.interface icon-theme Flat-Remix-Blue-Dark
gsettings set org.gnome.desktop.interface gtk-theme Flat-Remix-GTK-Blue-Darkest-Solid-NoBorder
```

```bash
# To .zshenv
export GTK2_RC_FILES=$HOME/.config/gtk-2.0/gtkrc-2.0
export GTK_THEME=Flat-Remix-GTK-Blue-Darkest-Solid-NoBorder
```

The `~/.config/gtk-2.0/gtkrc-2.0` is the same as `/etc/gtk-2.0/gtkrc`
> NOTE : The quotes "" are required only on gtk2 configs

```bash
# Names are themes directory names
gtk-icon-theme-name = "Flat-Remix-Blue-Dark"
gtk-theme-name = "Flat-Remix-GTK-Blue-Darkest-Solid-NoBorder"
#gtk-font-name = "Sans 18"
gtk-button-images = 1
gtk-menu-images = 1
```

And `~/.config/gtk-3.0/settings.ini` is the same as `/etc/gtk-3.0/settings.ini`
> NOTE : The quotes must be omitted from gtk3 config files unless there is a space
> Like the `gtk-font-name` option

```bash
[Settings]
gtk-icon-theme-name = Flat-Remix-Blue-Dark
gtk-theme-name = Flat-Remix-GTK-Blue-Darkest-Solid-NoBorder
gtk-font-name = "Sans 18"
gtk-button-images = 1
gtk-menu-images = 1
```

## Programming
compiling gtk :
	in_bash:  gcc file.c -o file `pkg-config --libs --cflags gtk+-2.0`
	in_fish: eval gcc file.c -o file (pkg-config --libs --clfags gtk+-2.0`

	to compile gtk 3.0 replace 2.0 with 3.0.

includeing gtk :
	#include <gtk/gtk.h>
code :
	starting gtk:
		gtk_init(&argc, &argv);

	creating gtk window:
		GtkWidget *wind_var = gtk_window_new (GTK_WINDOW_TOPLEVEL);

	unhide every widget or it won't show:
		gtk_widget_show (wind_var);

	call the main gtk function:
		gtk_main ():

	creating gtk button:
		GtkWidget *btn_var = gtk_button_new_with_label ("button text here");

	putting the button on its container:
		gtk_container_add (GTK_CONTAINER (wind_var), btn);

	show every thing on the window:
		gtk_widget_show_all (wind_var);

	making the window close by button press, we need to make a handler function to handl the exit signal:
		void exit_func(GtkWidget *window_var, gpointer ptr) {
			gtk_main_quit();
		}

	adding signal capturing function to the main this one will connect the click event with the callback of the exit function:
		g_signal_connect (button0_var, "clicked", G_CALLBACK (exit_func), NULL);

	adding exit handler on the x button (at the to right):
		g_signal_connect (window_var, "delete event", G_CALLBACK(exit_func), NULL);

	adding more items & in order to do that we need a box or table since gtk windows can't handel more than one widget at once:

	lets create the box (a vertical one "vbox" the fist arg is same_space for all widgets or not in this case FALSE means no, and the second one is the spcae between each one in this case it's 5pixels):
		GtkWidget *box_var = gtk_vbox_new (FALSE, 5);

	now to adding stuff to the box instead of the window as we did before which was kide of wrong:
		gtk_box_pack_start (GTK_BOX (box_var), lbl, TRUE, TRUE, 0);

	creating a label:
		GtkWidget *label_var = gtk_label_new ("Options :");



# QT

## Scaling

```bash
export QT_ENABLE_HIGHDPI_SCALING=1
export QT_AUTO_SCREEN_SCALE_FACTOR=2
export QT_SCALE_FACTOR=1 picard
```

## Theming

To theme Qt applications install `qt5ct` if you want to manually choose colors; Or use the recommended way of installing `qt5-styleplugins` to match the system's Gtk theme which (looks much much better)

### qt5ct

```bash
pacman -S qt5ct

# To .zshenv
export The QT_QPA_PLATFORMTHEME=qt5ct
```

### qt5-styleplugins (Recommended)

```bash
pacman -S qt5-styleplugins

# To .zshenv
export The QT_QPA_PLATFORMTHEME=gtk2

# Then create .config/Trolltech.conf
[Qt]
style=GTK+
```

