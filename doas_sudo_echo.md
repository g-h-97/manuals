

# The `tee` Method

```bash
echo "text" | tee /path/to/file
echo > /pathe/to/file

echo "text" | doas tee /path/to/file
```


```bash
echo "text" | tee -a /path/to/file
echo >> /pathe/to/file

echo "text" | doas tee -a /path/to/file
```

# The subshell Method

```bash
sudo sh -c "echo 'something' >> /etc/privilegedfile"
```
