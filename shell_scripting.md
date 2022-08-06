

# Update Line Without clear

> Source: https://stackoverflow.com/questions/12628327/how-to-show-and-update-echo-on-same-line

This trick allow you to update output line without clearing the terminal since the user might have some important output the he wants to keep (Anoying in ST), The following is two ways of doing this by putting the `Carriage Return` in / out side the echo string ( Must be escaped if outside )

```
i=0;while [ $i -lt 9999 ];do i=$(($i+1)) && echo -ne "text...$i\r" && sleep 1;done
i=0;while [ $i -lt 9999 ];do i=$(($i+1)) && echo -ne "text...$i"\\r && sleep 1;done
```

Also you can use `printf` instead of `echo` with is a more standard way of doing it

```
i=0;while [ $i -lt 9999 ];do i=$(($i+1)) && printf "text...$i\r" && sleep 1;done
```

# Output Color

```
\033[[COLOR]m
```

Where `[COLOR]` is and ANSI color such as

```
No Color     0
Black        0;30     Dark Gray     1;30
Red          0;31     Light Red     1;31
Green        0;32     Light Green   1;32
Brown/Orange 0;33     Yellow        1;33
Blue         0;34     Light Blue    1;34
Purple       0;35     Light Purple  1;35
Cyan         0;36     Light Cyan    1;36
Light Gray   0;37     White         1;37
```

Here is a `while` loop that outputs the first `8` colors, although it was intended to output all of the `16` color (Bug)

```
i=0;j=0;color="\033[${i};3${j}m";while [ $i -le 1 ];do while [ $j -le 7 ];do color="\033[${i};3${j}m";printf "${color}text" && j=$(($j+1)) && sleep 1;done && i=$(($i+1)) && sleep 1;done
```

However here is a `for` loop that works perfectly fine, the first one outputs the `text` next to each other while the second updates the line while changing the color (Great Effect)

```
for i in {0..1};do for j in {0..7};do color="\033[${i};3${j}m";printf "${color}text" && sleep 1;done;sleep 1;done
for i in {0..1};do for j in {0..7};do color="\033[${i};3${j}m";printf "${color}text\r" && sleep 1;done;sleep 1;done
```

# Redirections

Standard output and standard error to a file

`[CMD] > out_and_err 2>&1` == `[CMD] &> out_and_err`

Append

`[CMD] >> out_and_err 2>&1` == `[CMD] &>> out_and_err`

