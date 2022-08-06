
# yes / no dialog box

```bash
dialog --default-button "no" --yesno "This will erase the entire disk . Please proceed with caution" 0 0
```

# two input fileds with password

using `--and-widget` to stop fleckering

```bash
dialog --inputbox "Enter somthing :" 0 0 --and-widget --inputbox "Enter somthing else :" 0 0 \
--title " Password : " --passwordbox " Please set root password : " 0 0
```


# for password taking

```bash
dialog --title " Password : " --passwordbox " Please set root password : " 0 0
```

# buildlist (two columns)

```bash
dialog --buildlist "text" 0 0 0 "1" "item1" "off" \
 "2" "item2" "on" \
 "3" "item3" "off"
```

# creating a check list

```bash
dialog --default-item 2 --checklist "Select:" 0 0 5 \
  1 "First element" off \
  2 "Second element" off \
  3 "Third element" off
```

# creating radio list

```bash
dialog --radiolist "Select items:" 0 0 0 \
  1 "Choice number one" Off \
  2 "Choice number two" on \
  3 "Choice number three" off \
  4 "Choice number four" Off
```

# variables

var=$(dialog --stdout --inputbox "Enter var :" 0 0)


