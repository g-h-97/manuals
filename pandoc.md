
# Titles :

## Main Title :

## Sub Title :

### Inner Title :

> I am testing *pandoc* .

# Lists Numbers/Unnumbers :

- first line
+ second line

text

* third line

- my first ordered list :

1. first
2. second
3. third

- my second ordered list :

1. first
1. second
1. third

- nested lists :

1. This is the first numbered item.
2. This is the second.
i) this is a sub-point
ii) and another sub-point
1. This is the third item.  Note that the number I supplied is ignored

- ending a list manualy :

1. This is the first numbered item.
2. This is the second.
1. This is the third item.  Note that the number I supplied is ignored

<:!-- -->



# Figures

## Adding Figures

![Cute](figures/413px-Keepy-small.png){#fig:cute}

![](figures/Docker-logo.png){#fig:dockerlogo width=50%}

![my caption](./figures/myimage.png){ width=250px }
![my caption](./figures/myimage.png){ height=250px }
<!-- in html and css only -->
<img src="./figures/myimage.png" alt="my caption" style="width: 250px;"/>
<img src="./figures/myimage.png" alt="my caption" style="height: 250px;"/>

## Referencing

![Cute](figures/413px-Keepy-small.png){#fig:cute}

Reference a figure see this figure [@fig:cute]

The latex way can also be used

![my great image\label{fig-my-great-img}](image_great.jpg)

In Fig.\ref{fig-my-great-img}, I show a great image.

## No Floating Figures

By default latex puts figures where ever it thinks they should go based on some ? calculations. However in some cases we want then be exactly where we declare them on the markdown file; In order to achieve this create a file say `no_float.tex` with the content below and add this to your `pandoc` PDF compilation command line file `-H /path/to/no_float.tex`.

```tex
\usepackage{float}
\let\origfigure\figure
\let\endorigfigure\endfigure
\renewenvironment{figure}[1][2] {
    \expandafter\origfigure\expandafter[H]
} {
    \endorigfigure
}
```



# Code Blocks :

- 3 backticks at the top and bottom for codeblocks

```cpp
#include <stdio.h>
int main() {
    printf("Hello, world!\n");
    return 0;
}
```

- refrence code blocks as shown bellow

```{#lst:code .haskell .numberLines startFrom="10" caption="Listing caption"}
main :: IO ()
main = putStrLn "Hello World!"
```

You can list all supported highlighting languages with :

```bash
pandoc --list-highlight-languages
```

This is the full list as of 31-10-2020 :

abc
asn1
asp
ats
awk
actionscript
ada
agda
alertindent
apache
bash
bibtex
boo
c
cs
cpp
cmake
css
changelog
clojure
coffee
coldfusion
commonlisp
curry
d
dtd
default
diff
djangotemplate
dockerfile
doxygen
doxygenlua
eiffel
elixir
elm
email
erlang
fsharp
fortran
gcc
glsl
gnuassembler
m4
go
html
hamlet
haskell
haxe
ini
isocpp
idris
fasm
nasm
j
json
jsp
java
javascript
javascriptreact
javadoc
julia
kotlin
llvm
latex
lex
lilypond
literatecurry
literatehaskell
lua
mips
makefile
markdown
mathematica
matlab
maxima
mediawiki
metafont
modelines
modula2
modula3
monobasic
mustache
ocaml
objectivec
objectivecpp
octave
opencl
php
povray
pascal
perl
pike
postscript
powershell
prolog
protobuf
pure
purebasic
python
qml
r
relaxng
relaxngcompact
roff
ruby
rhtml
rust
sgml
sml
sql
sqlmysql
sqlpostgresql
scala
scheme
stata
tcl
tcsh
texinfo
mandoc
typescript
vhdl
verilog
xml
xul
yaml
yacc
zsh
dot
noweb
rest
sci
sed
xorg
xslt

# Sectionref :

Section {#sec:section}

# Footnotes :

Here is a footnote reference,[^1] and another.[^longnote]

[^1]: Here is the footnote.

[^longnote]: Here's one with multiple blocks.

- inline notes start with caret sign shift+6 and open square bracket and end with square bracket

Here is an inline note.^[Inlines notes are easier to write, since
you don't have to pick an identifier and move down to type the
note.]

# Tables :

- create table and refrence is as shown :

a   b   c
--- --- ---
1   2   3
4   5   6

: Caption {#tbl:label}

- another table :

  Column A    Column B    Column C
  ---------  ----------  ---------
  Category 1    High        100.00
  Category 2    High         80.50
  ---------  ----------  ---------

- multiline table :

  ----------------------------------
  Column A    Column B      Column C
  ---------  ----------  -----------
  Category 1    High        100.00
  High         95.00

  Category 2    High         80.50
  High         82.50
  ----------------------------------


-------------------------------------------------------------
 Centered   Default           Right Left
  Header    Aligned         Aligned Aligned
----------- ------- --------------- -------------------------
   First    row                12.0 Example of a row that
                                    spans multiple lines.

  Second    row                 5.0 Here's another one. Note
                                    the blank line between
                                    rows.
-------------------------------------------------------------

* grid tables :

  +---------------+---------------+--------------------+
  | Fruit         | Price         | Advantages         |
  +===============+===============+====================+
  | Bananas       | $1.34         | - built-in wrapper |
  |               |               | - bright color     |
  +---------------+---------------+--------------------+
  | Oranges       | $2.10         | - cures scurvy     |
  |               |               | - tasty            |
  +---------------+---------------+--------------------+

  +-----------+----------+-----------+
  |Column A   |Column B  |   Column C|
  +===========+==========+===========+
  |Category 1 |100.00    | - point A |
  |           |          | - point B |
  +-----------+----------+-----------+
  |Category 2 | 85.00    | - point C |
  |           |          | - point D |
  +-----------+----------+-----------+

* pipe tables :

  | Default | left  | Center | Right  |
  |---------|:------|:------:|-------:|
  |   High  | Cat 1 | A      | 100.00 |
  |   High  | Cat 2 | B      |  85.50 |
  |   Low   | Cat 3 | C      |  80.00 |



# Equations :

- equations start with doubl $ and end with doubl $
- you can refrence the as shown down bollow

$$ p = np $${#eq:briank}

- subscripts
* added whit a underscore _

$$p_p$$

* superscripts
* added with caret sign ^

$$P^p$$

- long sub/super scripts
- done by opening {} after the _ **subscripts** or ^ **superscripts**
* like so t _ {n+1} or t ^ {n+1} just remove the spaces

$$t_{n+1} = t^{n+1}$$

- how to do equations properly :

The formula, $y=mx+c$, is displayed inline.
Some symbols and equations (such as
$\sum{x}$ or $\frac{1}{2}$) are rescaled
to prevent disruptions to the regular
line spacing.
For more voluminous equations (such as

$\sum{\frac{(\mu - \bar{x})^2}{n-1}}$),

some line spacing disruptions are unavoidable.
Math should then be displayed in displayed mode.
$$\\sum{\frac{(\mu - \bar{x})^2}{n-1}}$$


# How to refrence :

[@fig:label1;@fig:label2;...] or [@eq:label1;@eq:label2;...] or [@tbl:label1;@tbl:label2;...] or @fig:label or @eq:label or @tbl:label

# subscripts & superscripts in paragraph :

- if you are writing math check **Equations** section since it diffrent

* super by surounding the text that you want higher by ^

text^super^

- sub by surounding the text that you want lower by ~

text~sub~

# Horizontal lines :

paragraph1

* * *

paragraph2

- - -

paragraph3

_ _ _

paragraph4


# the most useful metadata atributes to use in the metadata.yaml file

---
title: " Big Title Here "
author: " Guenfaf Hicham "
date: "dd-mm-yyyy"
abstract: " abstract your work here"
keywords:
  - keyword1
  - keyword2
  - keyword3
lang: en
table-of-content: true
numbersections: true

papersize: a4
---

# you can change the `lang` tag on the text like so :
 ::: {lang=en-GB}
 > british english text here
 :::

 ::: {lang=fr-CA}
 > canadian french text here
 :::

# you text direction (right-to-left) or (left-to-right) :

  dir: rtl

# padding of the test with :
  geometry:
    - top=30mm
    - right=20mm
    - left=20mm
    - bottom=30mm

# add indentation to the begining of a paragragh instead of spacing between them :

  indent

# change spacing in the text :

  linestreach

# set the page size ( paper type ) :

  pagesize: a4, letter

# font type :

  fontfamily: libertinus, "Latin Modern"

# then choose the font you want from the family with :

  fontfamilyoptions:

# font size :

  fontsize: 11pt, 12pt...

# add aknowledgments at the end :

  thanks:

# add table of contents :

  toc

# add list of tables & list of figures :

  lof
  lot
