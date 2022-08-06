
# Compile dot

To compile your `*.dot` file use the `dot` CLI tool as follows

```bash
dot -T[FORMAT] [INPUT] -o [OUTPU]

# Example
dot -Tpng graph.dot -o graph.png
```

# DPI / Resolution

There are two methods to tune the Dots Per Inch `DPI` in the output graph, the first one is to use the `-Gdpi=` flag and the second one is to use `graph [ dpi = 600 ];` in your `dot` file

```dot
digraph {
    graph [ dpi = 600 ];
    a -> b -> c
    b -> d
    a -> a[label="oh!"]
}
```

# Aggregate arrow heads

> Source: https://mike42.me/blog/2015-02-how-to-merge-edges-in-graphviz

Just create a node that is invisibly small and point the headless edges to it, then point that to the main node with a head of any type.

```dot
digraph mygraph {
    hidden [shape=point, width=0.01, height=0.01]
    { a b c d } -> hidden [dir=none]
    hidden -> e
}
```
